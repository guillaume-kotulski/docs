---
id: entities
title: Entities
---

An entity is an object that can be seen as an instance of a [dataclass](dataclasses.md), like a record of the table matching the dataclass in its associated [datastore](datastores.md). However, an entity also contains data correlated to the database related to the datastore. The purpose of the entity is to manage data (create, update, delete). When an entity reference is obtained by means of an entity selection, it retains information about the entity selection which allows iteration through the selection.

## Creating an entity  

There are two ways to create a new entity in a dataclass:

*	Since entities are references to database records, you can create entities by creating records using the "classic" 4D language and then reference them with ORDA methods such as `entity.next( )` or `entitySelection.first( )`.
*	You can also create an entity using the dataClass.new( ) method.

Keep in mind that the entity is only created in memory. If you want to add it to the datastore, you must call the `entity.save( )` method.

Entity attributes are directly available as properties of the entity object. For more information, please refer to [Using entity attributes](##using-entity-attributes).

For example, we want to create a new entity in the "Employee" dataclass in the current datastore with "John" and "Dupont" assigned to the firstname and name attributes:

```code4d
C_OBJECT($myEntity)
$myEntity:=ds.Employee.new() //Create a new object of the entity type
$myEntity.name:="Dupont" // assign 'Dupont' to the 'name' attribute
$myEntity.firstname:="John" //assign 'John' to the 'firstname' attribute
$myEntity.save() //save the entity
```

>An entity is defined only in the process where it was created. You cannot, for example, store a reference to an entity in an interprocess variable and use it in another process. 

## Entities and references 
 
An entity contains a reference to a 4D record. Different entities can reference the same 4D record. Also, since an entity can be stored in a 4D object variable, different variables can contain a reference to the same entity.

If you execute the following code:

```code4d
 C_OBJECT($e1;$e2)
 $e1:=ds.Employee.get(1) //access the employee with ID 1
 $e2:=$e1
 $e1.name:="Hammer"
  //both variables $e1 and $e2 share the reference to the same entity
  //$e2.name contains "Hammer"
```

This is illustrated by the following graphic:

![](assets/en/Orda/entityRef1.png)

Now if you execute:

```code4d
 C_OBJECT($e1;$e2)
 $e1:=ds.Employee.get(1)
 $e2:=ds.Employee.get(1)
 $e1.name:="Hammer"
  //variable $e1 contains a reference to an entity
  //variable $e2 contains another reference to another entity
  //$e2.name contains "smith"
```

This is illustrated by the following graphic:

![](assets/en/Orda/entityRef2.png)

Note however that entities refer to the same record. In all cases, if you call the `entity.save( )` method, the record will be updated (except in case of conflict, see [Entity locking](entityLocking.md)).

In fact, $e1 and $e2 is not the entity itself, but a reference to the entity. It means that you can pass it directly to any function or method, and it will act like a pointer, and faster than a 4D pointer. For example:

```code4d
 For each($entity;$selection)
    do_Capitalize($entity)
 End for each
```
 
And the function is:

```code4d
 $entity:=$1
 $name:=$entity.lastname
 If(Not($name=Null))
    $name:=Uppercase(Substring($name;1;1))+Lowercase(Substring($name;2))
 End if
 $entity.lastname:=$name
```
 
You can handle entities like any other object in 4D and pass their references directly as parameters.

>With the entities, there is no concept of "current record" as in the classic 4D language. You can use as many entities as you need, at the same time. There is also no automatic lock on an entity (see Entity locking). When an entity is loaded, it uses the 'Lazy loading' mechanism, which means that only the needed information is loaded. Nevertheless, in client/server, the entity can be automatically loaded directly if necessary.

## Using entity attributes  

Entity attributes store data and map corresponding fields in the corresponding table. Entity attributes of the storage kind can be set or get as simple properties of the entity object, while entity of the **relatedEntity** or **relatedEntities** kind will return an entity or an entity selection.

>For more information on the attribute kind, please refer to the [Storage attributes and Relation attributes](dataclasses.md#storage-attributes-and-relation-attributes) paragraph.

For example, to set a storage attribute:

```code4d
 $entity:=ds.Employee.get(1) //get employee attribute with ID 1
 $name:=entity.lastname //get the employee name, e.g. "Smith"
 entity.lastname:="Jones" //set the employee name
```

>Pictures attributes cannot be assigned directly with a given path in an entity.

Accessing a related attribute depends on the attribute kind. For example, with the following structure:

![](assets/en/Orda/entityAttributes.png)

You can access data through the related object(s):

```code4d
 $entity:=ds.Project.all().first().theClient //get the Company entity associated to the project
 $EntitySel:=ds.Company.all().first().companyProjects //get the selection of projects for the company
```

Note that both *theClient* and *companyProjects* in the above example are primary relation attributes and represent a direct relationship between the two dataclasses. However, relation attributes can also be built upon paths through relationships at several levels, including circular references. For example, consider the following structure:

![](assets/en/Orda/entityAttributes2.png)

Each employee can be a manager and can have a manager. To get the manager of the manager of an employee, you can simply write:

```code4d
 $myEmp:=ds.Employee.get(50)
 $manLev2:=$myEmp.manager.manager.lastname
```

## Assigning values to relation attributes  

In the ORDA architecture, relation attributes directly contain data related to entities:

*	An N->1 type relation attribute (**relatedEntity** kind) contains an entity
*	A 1->N type relation attribute (**relatedEntities** kind) contains an entity selection

Let's look at the following (simplified) structure:

![](assets/en/Orda/entityAttributes3.png)

In this example, an entity in the "Employee" dataclass contains an object of type Entity in the "employer" attribute (or a null value). An entity in the "Company" dataclass contains an object of type EntitySelection in the "staff" attribute (or a null value).

>In ORDA, the Automatic or Manual property of relations has no effect.

To assign a value directly to the "employer" attribute, you must pass an existing entity from the "Company" dataclass. For example:

```code4d
 $emp:=ds.Employee.new() // create an employee
 $emp.lastname:="Smith" // assign a value to an attribute
 $emp.employer:=ds.Company.query("name =:1";"4D")[0]  //assign a company entity
 $emp.save()
```

4D provides an additional facility for entering a relation attribute for an N entity related to a "1" entity: you pass the primary key of the "1" entity directly when assigning a value to the relation attribute. For this to work, you pass data of type Number or Text (the primary key value) to the relation attribute. 4D then automatically takes care of searching for the corresponding entity in the dataclass. For example:

```code4d
 $emp:=ds.Employee.new()
 $emp.lastname:="Wesson"
 $emp.employer:=2 // assign a primary key to the relation attribute
  //4D looks for the company whose primary key (in this case, its ID) is 2
  //and assigns it to the employee
 $emp.save()
```

This is particularly useful when you are importing large amounts of data from a relational database. This type of import usually contains an "ID" column, which references a primary key that you can then assign directly to a relation attribute.

This also means that you can assign primary keys in the N entities without corresponding entities having already been created in the 1 datastore class. If you assign a primary key that does not exist in the related datastore class, it is nevertheless stored and assigned by 4D as soon as this "1" entity is created.

You can assign or modify the value of a "1" related entity attribute from the "N" dataclass directly through the related attribute. For example, if you want to modify the name attribute of a related Company entity of an Employee entity, you can write:

```code4d
 $emp:=ds.Employee.get(2) // load the Employee entity with primary key 2
 $emp.employer.name:="4D, Inc." //modify the name attribute of the related Company
 $emp.employer.save() //save the related attribute
  //the related entity is updated
```

## About the entity object  

The entity object itself cannot be copied as an object:

```code4d
 $myentity:=OB Copy(ds.Employee.get(1)) //returns null
```

The entity properties are however enumerable:

```code4d
 ARRAY TEXT($prop;0)
 OB GET PROPERTY NAMES(ds.Employee.get(1);$prop)
  //$prop contains the names of all the entity attributes
```

For export needs, you can however convert an entity to a standard object using the `entity.toObject( )` method. You can then export the entity as JSON, for example:

```code4d
 C_OBJECT($entity_json)
 $entity_json:=JSON Stringify($myentity.toObject()) //returns the entity as JSON
```