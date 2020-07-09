# Custo - great for storing Customer/PII data
basic system for defining schemas, storing and retrieving documents, and rules execution

the system is intended to be a server-side MVC framework consisting of-

Model - 
a way to specify a model for information to be stored and how to modify it. event sourcing with checkpointing should be encouraged here. implications are that the model should be validated and is a living document which can be modified. the model is metadata about the thing you want to store/manage.

View - 
a simple transformation that turns the model into a LOGICAL view, not a physical one. This logical view is presented to a client app which decides how best to perform the physical rendering. the logical view can specify grouping, filtering and ordering of attributes of the model.

Controller - 
rules based execution about what is allowed to be changed, how it can be changed etc. this will result in either filtering the view, or limiting or rejecting data updates to objects specified by the model.


What is needed for this to work-

schema editing tools and representation stored for each type. consider using tools such as -

https://openapi.tools/

https://www.openapi4j.org/schema-validator.html

a RESTful interface/controller for creating and updating these models.

In previous work, I created 'preferences' and 'selections' - where 'preferences' were the model for a customer's preferences, and the act of selecting these on a web site generated 'selections' these selections semantically indicated that at a certain point in time, a customer had made certain selections on their 'allowable' preferences.

allowable preferences gets us into rules selection and another part of the system has to be a way to specify highly performant rules to filter/select those preferences we need. these rules in the higher level customer management arena may not make as much sense but other rules, such as validation, etc. may. they are also a way of abstracting the filtering process, so may be an effective way of specifying a further 'where clause' - will see...

a flexible document database, such as couchbase. it supports XDCR, with multiple one way replications and can perform actions against its held data to modify it in the case of a schema change. it also does not care about schema intrinsically, so needs external tools to add constraints in that dept.

kubernetes platform for running a cluster

operator for handling changes to the cluster

security is important so likely RBAC or entitlements, cert authority, and user/system directory for authentication

