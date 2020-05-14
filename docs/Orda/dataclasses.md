---
id: dataclasses
title: Dataclasses
---

## Definition  

Dataclasses provide object interfaces to database tables. All dataclasses in a 4D application are available as a property of the [ds](glossary.md#ds) datastore. For example, consider the following table in the 4D structure.

![](assets/en/Orda/companyTable.png)

The `Company` table is automatically available as a dataclass in the ds [datastore](glossary.md#datastore). You can write:

```code4d 
C_OBJECT(compClass)
 compClass:=ds.Company
```

This code assigns to *compClass* a reference to the Company dataclass.

A dataclass object can contain:

*	attributes
*	relation attributes

The dataclass offers an abstraction of the physical database and allows handling a conceptual data model. The dataclass is the only means to query the datastore. A query is done from a single dataclass. Queries are built around attributes and relation attribute names of the dataclasses. So the relation attributes are the means to involve several linked tables in a query.

## Dataclass attributes  

Dataclass attributes are available as properties of their respective classes. For example:

```code4d 
 nameAttribute:=ds.Company.name //reference to class attribute
 revenuesAttribute:=ds.Company["revenues"] //alternate way
```

This code assigns to nameAttribute and revenuesAttribute references to the name and revenues attributes of the Company class. This syntax does NOT return values held inside of the attribute, but instead returns references to the attributes themselves. To handle values, you need to go through [Entities](entities.md).

>Dataclass attributes are objects which have properties, detailed in the ORDA - DataClassAttribute section.

### Storage attributes and Relation attributes  

Dataclass attributes come in several kinds: storage, relatedEntity, and relatedEntities. Attributes that are scalar (*i.e.*, provide only a single value) support the standard 4D data type (longint, text, object, etc.).

*	A **storage attribute** is equivalent to a field in the 4D database and can be indexed. Values assigned to a storage attribute are stored as part of the entity when it is saved. When a storage attribute is accessed, its value comes directly from the datastore. Storage attributes are the most basic building block of an entity and are defined by name and data type.
*	A **relation attribute** provides access to other entities. Relation attributes can result in either a single entity (or no entity) or an entity selection (0 to N entities). Relation attributes are built upon "classic" relations in the relational structure to provide direct access to related entity or related entities. Relation attributes are directy available in ORDA using their names.

For example, consider the following partial database structure and the relation properties:

![](assets/en/Orda/relationProperties.png)

All storage attributes will be automatically available:

*	in the Project dataclass: "ID", "name", and "companyID"
*	in the Company dataclass: "ID", "name", and "discount"

In addition, the following relation attributes will also be automatically available:

*	in the Project dataclass: **theClient** attribute, of the "relatedEntity" kind; there is at most one Company for each Project (the client)
*	in the Company dataclass: **companyProjects** attribute, of the "relatedEntities" kind; for each Company there is any number of related Projects.

>The Manual or Automatic property of a database relation has no effect in ORDA.

All dataclass attributes are exposed as properties of the dataclass:

![](assets/en/Orda/dataclassProperties.png)

Keep in mind that these objects describe attributes, but do not give access to data. Reading or writing data is done through entity objects. For more information on how to use related attributes in entities, please refer to Using entity attributes.

### Attribute names and attribute references
  
Some ORDA methods accept string references as attribute names and can also accept attribute references. For example, consider the following:

```code4d 
localPeople:=ds.Employee.query("zipCode = 95113")
lastNames:=localPeople.toCollection("lastname")
``` 

This code defines an entity selection of people in the 95113 zip code. It then produces a collection of last names. In place of a string value representing an attribute, you may also use an attribute reference like this:

```code4d 
lastNameAtt:=ds.Employee.lastname
localPeople:=ds.Employee.query("zipCode = 95113")
lastNames:=localPeople.toCollection(lastNameAtt)
``` 

## About the dataclass object
  
The dataclass object itself cannot be copied as an object:

```code4d 
$mydataclass:=OB Copy(ds.Employee) //returns null
```

The dataclass properties are however enumerable:

```code4d 
ARRAY TEXT($prop;0)
OB GET PROPERTY NAMES(ds.Employee;$prop)
//$prop contains the names of all the dataclasse attributes
```