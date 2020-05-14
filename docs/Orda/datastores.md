---
id: datastores
title: Datastores
---

## What is a datastore?
  
A datastore is the interface object provided by ORDA to reference and access a database. A datastore is made of a model and data:

The model contains and describes all the dataclasses that make up the datastore. It is independant from the underlying database itself.

Data refers to the information that is going to be used and stored in this model. For example, names, addresses, and birthdates of employees are pieces of data that you can work with in a datastore.

When handled through the code, the datastore is an object whose properties are all of the defined dataclasses. A datastore references only a single local or remote database.

4D allows you to handle the following datastores:

the local datastore, based on the current 4D database, returned by the ds command (the main datastore).
one or more remote datastore(s) exposed as REST resources in remote 4D databases, returned by the Open datastore command. 

>Datastore related methods and properties are detailed in the ORDA - DataStore chapter of the Language manual.

### Datastore access architecture  
A datastore exposed on a 4D Server application can be accessed simultaneously through different clients:

4D remote applications using ORDA to access the main datastore with the ds command. Note that the 4D remote application can still access the database in classic mode. These accesses are handed by the 4D application server. 

Other 4D applications (4D remote, 4D Server) opening a session on the remote datastore through the Open datastore command. These accesses are handed by the HTTP REST server. 

4D for iOS queries for updating iOS applications. These accesses are handed by the HTTP server. 

## Datastore mapping  

When you call a datastore using the ds or the Open datastore command, 4D automatically references each exposed table and field of the corresponding 4D database as attributes of the returned object:

*	Tables are mapped to dataclasses.
*	Fields are mapped to storage attributes.
*	Records are mapped to entities.
*	Relations are mapped to relation attributes - relation names, defined in the Structure editor, are used as relation attribute names.

![](assets/en/Orda/datastoreMapping.png)
 
The following rules are applied during conversion:

*	Only tables and fields with the "Exposed as REST resource" property are available.

*	Table, field, and relation names are mapped to object property names. If you want to use "dot notation" in ORDA, make sure that such names comply with general object naming rules, as explained in the [Object property](Concepts/object.md#object-properties) section.

>The "Manual" or "Automatic" property of relations has no effect in ORDA.

*	A datastore only references tables with a single primary key (see Primary keys). The following tables are not referenced:
	*	Tables without a primary key
	*	Tables with composite primary keys.
*	BLOB type attributes are not managed in the datastore. BLOB type attributes are returned as Null in entities and cannot be assigned.

### Model update  

Any modifications applied at the level of the database structure invalidate the current ORDA model layer. These modifications include:

*	adding or removing a table, a field, or a relation
*	renaming of a table, a field, or a relation
*	changing a core property of a field (type, unique, index, autoincrement, null value support)

When the current ORDA model layer has been invalidated, it is automatically reloaded and updated in subsequent calls of the local ds datastore on 4D and 4D Server. Note that existing references to ORDA objects such as entities or entity selections will continue to use the model from which they have been created, until they are regenerated.

However, the updated ORDA model layer is not automatically available in the following contexts:

*	a remote 4D application connected to 4D Server -- the remote application must reconnect to the server. 
*	a remote datastore (opened using Open datastore, see below) -- a new session must be opened. 

## Using remote datastores  

When you work with a remote datastore referenced through calls to the Open datastore command, the connection between the requesting processes and the remote datastore is handled via sessions. 

 
### Opening sessions  

When a 4D application (*i.e.* a process) opens an external datastore using the Open datastore command, a session in created on the remote datastore to handle the connection. This session is identified using a internal session ID which is associated to the localID on the 4D application. This session automatically manages access to data, entity selections, or entities. 

The localID is local to the machine that connects to the remote datastore, which means:

*	If other processes of the same application need to access the same remote datastore, they can use the same localID and thus, share the same session. 
*	If another process of the same application opens the same remote datastore but with another localID, it will create a new session on the remote datastore.
*	If another machine connects to the same remote datastore with the same localID, it will create another session with another cookie.

These principles are illustrated in the following graphics:

![](assets/en/Orda/sessions.png)

### Viewing sessions  

Processes that manage sessions for datastore access are shown in the 4D Server administration window:

*	name: "REST Handler: <process name>" 
*	type: HTTP Server Worker type
*	session: session name is the user name passed to the Open datastore command.

In the following example, two processes are running for the same session:

![](assets/en/Orda/sessionAdmin.png)

### Locking and transactions  

ORDA features related to entity locking and transaction are managed at process level in remote datastores, just like in ORDA client/server mode:

*	If a process locks an entity from a remote datastore, the entity is locked for all other processes, even when these processes share the same session (see Entity locking). If several entities pointing to a same record have been locked in a process, they must be all unlocked in the process to remove the lock. If a lock has been put on an entity, the lock is removed when there is no more reference to this entity in memory. 
*	Transactions can be started, validated or cancelled separately on each remote datastore using the dataStore.startTransaction( ), dataStore.cancelTransaction( ), and dataStore.validateTransaction( ) methods. They do not impact other datastores. 
*	Classic 4D language commands (START TRANSACTION, VALIDATE TRANSACTION, CANCEL TRANSACTION) only apply to the main datastore (returned by ds).
If an entity from a remote datastore is hold by a transaction in a process, other processes cannot update it, even if these processes share the same session. 
*	Locks on entities are removed and transactions are rollbacked:
	*	when the process is killed.
	*	when the session is closed on the server
	*	when the session is killed from the server administration window.
 
### Closing sessions  

A session is automatically closed by 4D when there has been no activity during its timeout period. The default timeout is 60 mn, but this value can be modified using the connectionInfo parameter of the Open datastore command. 

If a request is sent to the remote datastore after the session has been closed, it is automatically re-created if possible (license available, server not stopped...). However, keep in mind that the context of the session regarding locks and transactions is lost (see above). 

## About the datastore object  

The datastore object itself cannot be copied as an object:

```code4d 
$mydatastore:=OB Copy(ds) //returns null
```


The datastore properties are however enumerable:


```code4d 
 ARRAY TEXT($prop;0)
 OB GET PROPERTY NAMES(ds;$prop)
  //$prop contains the names of all the dataclasses
```