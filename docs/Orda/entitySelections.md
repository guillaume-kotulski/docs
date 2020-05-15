---
id: entitySelections
title: Entity selections
---

## Overview  

An entity selection is an [object](Concepts/dt_object.md) containing one or more reference(s) to entities belonging to the same dataclass. An entity selection can contain 0, 1 or X entities from the dataclass -- where X can represent the total number of entities contained in the dataclass. Entity selections can be "sorted" or "unsorted" (this point is discussed below). 

Entity selections are usually created using a query or returned from a relation attribute. For example:

```code4d
 brokers:=ds.Person.query("personType = broker")
```

This code returns in *brokers* all the people of type broker. To access an entity of the selection, use syntax similar to accessing an element in a collection. For example:

```code4d
 theBroker:=brokers[0]  //Entity selections are 0 based
```

The `entitySelection.orderBy( )` method returns a new entity selection according to the supplied sort criteria. For example:

```code4d
 brokers:=brokers.orderBy("name") //returns a sorted selection
```

This code returns in *brokers* the same entity selection of Person entities, but sorted by name.

Alternatively, you can use a relation attribute to return an entity selection. For example:

```code4d
 brokers:=ds.Person.query("personType = broker")
 brokerCompanies:=brokers.myCompany
```

This code assigns to *brokerCompanies* all related companies of the people in the *brokers* entity selection, using the relation attribute *myCompany*. Using relation attributes on entity selections is a powerful and easy way to navigate up and down the chain of related entities.

To perform repeated actions to entities in an entity selection, like retrieving and modifying values of certain attributes, you can use the `For each...End for each` structure. For example:

```code4d
 C_OBJECT(emp)
 For each(emp;ds.Employees.all())
    If(emp.Country="UK")
       emp.salary:=emp.salary*1,03
       emp.save()
    End if
 End for each
```
 
 
 
## Creating an entity selection  

You can create an object of type entity selection as follows:

*	Querying the entities in a dataclass (see the `dataClass.query( )` method);

*	Using the `dataClass.all( )` method to select all the entities in a dataclass;

*	Using the `Create entity selection` command or the `dataClass.newSelection( )` method to create a blank entity collection object;

*	Using one of the various methods from the **ORDA - EntitySelection** theme that returns a new entity selection, such as `entitySelection.or( )`;

*	Using a relation attribute of type "related entities" (see below).

You can simultaneously create and use as many different entity selections as you want for a dataclass. Keep in mind that an entity selection only contains references to entities. Different entity selections can contain references to the same entities.

>An entity selection is only defined in the process where it was created. You cannot, for example, store a reference to an entity selection in an interprocess variable and use it in another process.

## Entity selections and attributes  

### Entity selections and Storage attributes  

All storage attributes (text, number, boolean, date) are available as properties of entity selections as well as entities. When used in conjunction with an entity selection, a scalar attribute returns a collection of scalar values. For example:

```code4d
 locals:=ds.Person.query("city = :1";"San Jose") //entity selection of people
 localEmails:=locals.emailAddress //collection of email addresses (strings)
```

This code returns in *localEmails* a collection of email addresses as strings.

### Entity selections and Relation attributes  

In addition to the variety of ways you can query, you can also use relation attributes as properties of entity selections to return new entity selections. For example, consider the following structure: 

![](assets/en/Orda/entitySelectionRelationAttributes.png)

```code4d
myParts:=ds.Part.query("ID < 100") //Return parts with ID less than 100
 $myInvoices:=myParts.invoiceItems.invoice
  //All invoices with at least one line item related to a part in myParts
```

The last line will return in $myInvoices an entity selection of all invoices that have at least one invoice item related to a part in the entity selection myParts. When a relation attribute is used as a property of an entity selection, the result is always another entity selection, even if only one entity is returned. When a relation attribute is used as a property of an entity selection and no entities are returned, the result is an empty entity selection, not null.

### Ordered vs Unordered entity selections  

Local entity selections can be ordered or unordered. Basically, both objects have similar functionality but there are some differences regarding their performance and available features. You can decide which type of entity selection to use according to your specific needs.

>The following entity selections are always ordered:
>
>*	entity selections returned by 4D Server to a remote client 
>*	entity selections built upon remote datastores.

### Comparing entity selection types  

*	Unordered entity selections are built upon bit tables in memory. An unordered entity selection contains one bit for every entity in the dataclass, regardless of whether the entity is actually in the selection. Each bit is equal to 1 or 0, to indicate whether or not the entity is included in the selection. It is a very compact representation for each entity.<p>
As a consequence, operations using unordered entity selections are very fast. Also, unordered entity selections are very economical in terms of memory space. The size of an unordered entity selection, in bytes, is always equal to the total number of entities in the dataclass divided by 8. For example, if you create an unordered entity selection for a dataclass containing 10,000 entities, it takes up 1,250 bytes, which is about 1.2K in RAM.<p>
On the other hand, unordered entity selections cannot be ordered. You cannot rely on the position of entities within the selection. Also, you cannot have more than one reference to the same entity in the selection: each entity can only be added once.

*	Ordered entity selections are built upon longint arrays (containing entity references) in memory. Each reference to an entity takes 4 bytes in memory. Processing and maintaining such selections takes more time and requires more memory space than unsorted selections.<p>
On the other hand, they can be ordered or reordered, and you can rely on entity positions. Also, you can add more than one reference to the same entity. 

The following table summarizes the main characteristics of each type of entity selection:

|Feature|Unordered entity selection|Ordered entity selection|
|---|---|---|
|Processing speed|very fast	|slower|
|Size in memory|very small	|larger|
|Can contain several references to an entity|no|yes|

For optimization reasons, by default 4D ORDA usually creates unordered entity selections, except when you use the `orderBy( )` method or use the appropriate options (see below). In this documentation, unless specified, "entity selection" usually refers to an "unordered entity selection".

### Creating ordered or unordered entity selections  

As mentioned above, by default ORDA creates and handles unordered entity selections as a result of operations such as queries or comparisons like and( ). Ordered entity selections are created only when necessary or when specifically requested using options.

Ordered entity selections are created in the following cases:

*	result of an `orderBy( )` on a selection (of any type) or an `orderBy( )` on a dataclass

*	result of the `newSelection( )` method with the `dk keep ordered` option

Unordered entity selections are created in the following cases:

*	result of a standard `query( )` on a selection (of any type) or a `query( )` on a dataclass,

*	result of the `newSelection( )` method without option,

*	result of any of the comparison methods, whatever the input selection types: `or( )`, `and( )`, `minus( )`.

Note that when an ordered entity selection becomes an unordered entity selection, any repeated entity references are removed.

If you want to transform an ordered entity selection to an unordered one, you can just apply an `and( )` operation to it, for example:

```code4d
  //mySel is an ordered entity selection
 mySel:=mySel.and(mySel)
  //mySel is now an unordered entity selection
```

## Client/server optimization  

4D provides an automatic optimization for ORDA requests that use entity selections or load entities in client/server configurations. This optimization speeds up the execution of your 4D application by reducing drastically the volume of information transmitted over the network. 

The following optimization mechanisms are implemented:

*	When a client requests an entity selection from the server, 4D automatically "learns" which attributes of the entity selection are actually used on the client side during the code execution, and builds a corresponding "optimization context". This context is attached to the entity selection and stores the used attributes. It will be dynamically updated if other attributes are used afterwards.

*	Subsequent requests sent to the server on the same entity selection automatically reuse the optimization context and only get necessary attributes from the server, which accelerates the processing. For example in an entity selection-based list box, the learning phase takes place during the display of the first rows, next rows display is very optimized. 

*	An existing optimization context can be passed as a property to another entity selection of the same dataclass, thus bypassing the learning phase and accelerating the application (see [Using the context property](#using-the-context-property) below). 

The following methods automatically associate the optimization context of the source entity selection to the returned entity selection:

*	`entitySelection.and( )`
*	`entitySelection.minus( )`
*	`entitySelection.or( )`
*	`entitySelection.orderBy( )`
*	`entitySelection.slice( )`
*	`entitySelection.drop( )`


**Example**

Given the following code:

```code4d
 $sel:=$ds.Employee.query("firstname = ab@")
 For each($e;$sel)
    $s:=$e.firstname+" "+$e.lastname+" works for "+$e.employer.name // $e.employer refers to Company table
 End for each
```

Thanks to the optimization, this request will only get data from used attributes (firstname, lastname, employer, employer.name) in $sel after a learning phase. 

 

### Using the context property

You can increase the benefits of the optimization by using the **context** property. This property references an optimization context "learned" for an entity selection. It can be passed as parameter to ORDA methods that return new entity selections, so that entity selections directly request used attributes to the server and bypass the learning phase.

A same optimization context property can be passed to unlimited number of entity selections on the same dataclass. All ORDA methods that handle entity selections support the **context** property (for example `dataClass.query( )` or `dataClass.all( )` method). Keep in mind, however, that a context is automatically updated when new attributes are used in other parts of the code. Reusing the same context in different codes could result in overloading the context and then, reduce its efficiency. 

>A similar mechanism is implemented for entities that are loaded, so that only used attributes are requested (see the `dataClass.get( )` method). 

 

**Example with `dataClass.query( )` method:**

```code4d
C_OBJECT($sel1;$sel2;$sel3;$sel4;$querysettings;$querysettings2)
 C_COLLECTION($data)
 $querysettings:=New object("context";"shortList")
 $querysettings2:=New object("context";"longList")
 
 $sel1:=ds.Employee.query("lastname = S@";$querysettings)
 $data:=extractData($sel1) // In extractData method an optimization is triggered and associated to context "shortList"
 
 $sel2:=ds.Employee.query("lastname = Sm@";$querysettings)
 $data:=extractData($sel2) // In extractData method the optimization associated to context "shortList" is applied
 
 $sel3:=ds.Employee.query("lastname = Smith";$querysettings2)
 $data:=extractDetailedData($sel3) // In extractDetailedData method an optimization is triggered and associated to context "longList"
 
 $sel4:=ds.Employee.query("lastname = Brown";$querysettings2)
 $data:=extractDetailedData($sel4) // In extractDetailedData method the optimization associated to context "longList" is applied
```

### Entity selection-based list box

Entity selection optimization is automatically applied to entity selection-based list boxes in client/server configurations, when displaying and scrolling a list box content: only the attributes displayed in the list box are requested from the server.

A specific "page mode" context is also provided when loading the current entity through the **Current item** property expression of the list box (see [Collection or entity selection type list boxes](FormObjects/listboxOverview.md#list-box-types)). This feature allows you to not overload the list box initial context in this case, especially if the "page" requests additional attributes. Note that only the use of **Current item** expression will create/use the page context (access through `entitySelection\[index]` will alter the entity selection context).

Subsequent requests to server sent by entity browsing methods will also support this optimization. The following methods automatically associate the optimization context of the source entity to the returned entity:

*	`entity.next( )`
*	`entity.first( )`
*	`entity.last( )`
*	`entity.previous( )`

For example, the following code loads the selected entity and allows browsing in the entity selection. Entities are loaded in a separate context and the list box initial context is left untouched:

```code4d
 $myEntity:=Form.currentElement //current item expression
  //... do something
 $myEntity:=$myEntity.next() //loads the next entity using the same context
```

## About the entity selection object 
 
The entity selection object itself cannot be copied as an object:

```code4d
 $myentitysel:=OB Copy(ds.Employee.all()) //returns null
``` 
 
The entity selection properties are however enumerable:

```code4d
 ARRAY TEXT($prop;0)
 OB GET PROPERTY NAMES(ds.Employee.all();$prop)
  //$prop contains the names of the entity selection properties
  //("length", 00", "01"...)
```