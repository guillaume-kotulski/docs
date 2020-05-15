---
id: entityLocking
title: Entity locking
---

You often need to manage possible conflicts that might arise when several users or processes load and attempt to modify the same entities at the same time. Record locking is a methodology used in relational databases to avoid inconsistent updates to data. The concept is to either lock a record upon read so that no other process can update it, or alternatively, to check when saving a record to verify that some other process hasn’t modified it since it was read. The former is referred to as **pessimistic record locking** and it ensures that a modified record can be written at the expense of locking records to other users. The latter is referred to as **optimistic record locking** and it trades the guarantee of write privileges to the record for the flexibility of deciding write privileges only if the record needs to be updated. In pessimistic record locking, the record is locked even if there is no need to update it. In optimistic record locking, the validity of a record’s modification is decided at update time.

ORDA provides you with two entity locking modes:

*	an automatic "optimistic" mode, suitable for most applications,

*	a "pessimistic" mode allowing you to lock entities prior to their access.

## Automatic optimistic lock  

This automatic mechanism is based on the concept of "optimistic locking" which is particularly suited to the issues of web applications. This concept is characterized by the following operating principles:

*	All entities can always be loaded in read-write; there is no *a priori* "locking" of entities.

*	Each entity has an internal locking stamp that is incremented each time it is saved.

*	When a user or process tries to save an entity using the `entity.save( )` method, 4D compares the stamp value of the entity to be saved with that of the entity found in the data (in the case of a modification):
	*	When the values match, the entity is saved and the internal stamp value is incremented.
	*	When the values do not match, it means that another user has modified this entity in the meantime. The save is not performed and an error is returned.

The following diagram illustrates optimistic locking:

1. Two processes load the same entity.<br><br>![](assets/en/Orda/optimisticLock1.png)

2. The first process modifies the entity and validates the change. The `entity.save( )` method is called. The 4D engine automatically compares the internal stamp value of the modified entity with that of the entity stored in the data. Since they match, the entity is saved and its stamp value is incremented.<br><br>![](assets/en/Orda/optimisticLock2.png)

3. The second process also modifies the loaded entity and validates its changes. The `entity.save( )` method is called. Since the stamp value of the modified entity does not match the one of the entity stored in the data, the save is not performed and an error is returned.<br><br>![](assets/en/Orda/optimisticLock3.png)


This can also be illustrated by the following code:

```code4d
 $person1:=ds.Person.get(1) //Reference to entity
 $person2:=ds.Person.get(1) //Other reference to same entity
 $person1.name:="Bill"
 $result:=$person1.save() //$result.success=true, change saved
 $person2.name:="William"
 $result:=$person2.save() //$result.success=false, change not saved
```

In this example, we assign to $person1 a reference to the person entity with a key of 1. Then, we assign another reference of the same entity to variable $person2. Using $person1, we change the first name of the person and save the entity. When we attempt to do the same thing with $person2, 4D checks to make sure the entity on disk is the same as when the reference in $person1 was first assigned. Since it isn't the same, it returns false in the success property and doesn’t save the second modification.

When this situation occurs, you can, for example, reload the entity from the disk using the `entity.reload( )` method so that you can try to make the modification again. The `entity.save( )` method also proposes an "automerge" option to save the entity in case processes modified attributes that were not the same.

## Pessimistic lock  

You can lock and unlock entities on demand when accessing data. When an entity is getting locked by a process, it is loaded in read/write in this process but it is locked for all other processes. The entity can only be loaded in read-only mode in these processes; its values cannot be edited or saved.

This feature is based upon two methods of the Entity class:

*	`entity.lock( )`
*	`entity.unlock( )`

For more information, please refer to the descriptions for these methods.


## Concurrent use of 4D classic locks and ORDA pessimistic locks  

Using both classic and ORDA commands to lock records is based upon the following principles:

*	A lock set with a classic 4D command on a record prevents ORDA to lock the entity matching the record.

*	A lock set with ORDA on an entity prevents classic 4D commands to lock the record matching the entity.

These principles are shown in the following diagram:

![](assets/en/Orda/concurrent1.png)

**Transaction locks** also apply to both classic and ORDA commands. In a multiprocess or a multi-user application, a lock set within a transaction on a record by a classic command will result in preventing any other processes to lock entities related to this record (or conversely), until the transaction is validated or canceled.

*	Example with a lock set by a classic command:<br><br>![](assets/en/Orda/concurrent2.png)

*	Example with a lock set by an ORDA method:<br><br>![](assets/en/Orda/concurrent3.png)

