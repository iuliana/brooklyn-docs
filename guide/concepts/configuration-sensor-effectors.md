---
title: Configuration, Sensors and Effectors
---

### Configuration

All entities contain a map of config information. This can contain arbitrary values, typically keyed under static `ConfigKey` fields on the `Entity` sub-class. These values are inherited, so setting a configuration value at the
application level will make it available in all entities underneath unless it is overridden.

Configuration is propagated when an application "goes live" (i.e. it becomes "managed", either explicitly or when its `start()` method is invoked), so config values must be set before this occurs. 

Configuration values can be specified in a configuration file (`brooklyn.cfg`)
to apply universally, and/or programmatically to a specific entity and its descendants 
by calling `.configure(KEY, VALUE)` in the entity spec when creating it.
There is also an `entity.config().set(KEY, VALUE)` method.

Additionally, many common configuration parameters are available as "flags" which can be supplied as Strings when constructing
the entity, in the form
`EntitySpec.create(MyEntity.class).configure("config1", "value1").configure("config2", "value2")`. 

Documentation of the flags available for individual entities can normally be found in the javadocs. 
The `@SetFromFlag` annotations on `ConfigKey` static field definitions
in the entity's interface is the recommended mechanism for exposing configuration options.


### Sensors and Effectors

***Sensors*** (activity information and notifications) and ***effectors*** (operations that can be invoked on the entity) are defined by entities as static fields on the `Entity` subclass.

Sensors can be updated by the entity or associated tasks – each update generates an event. An entity can subscribe to sensor events from itself or other entities.
A common pattern is for an entity to subscribe to its children (or for a group to subscribe to its members), to aggregate the sensor data and to respond to those events.

Effectors can be invoked by an entity's parent, and the invoker is able to track the execution of that effector. Effectors can also be invoked by other entities, but use this functionality with care to prevent too many managers!

An entity consists of a Java interface (used when interacting with the entity) and a Java class. For resilience, it is recommended to store 
the entity's state in attributes (see `getAttribute(AttributeKey)`). If internal fields are used then the data will be lost on brooklyn
restart, and may cause problems if the entity is to be moved to a different brooklyn management node.

