---
title: Java Entities
partial-summary-depth: 1
---

Java blueprints are powerful, but also rather more difficult to write than YAML.
Advanced Java skills are required.



The main uses of Java-based blueprints are:

* Integration with a service's API (e.g. for an on-line DNS service). This could take advantage of
  existing Java-based clients, or of Java's flexibility to chain together multiple calls.
* Complex management logic, for example when the best practices for adding/removing nodes from a
  cluster is fiddly and has many conditionals.
* Where the developer has a strong preference for Java. Anything that can be done in YAML can be done in
  the Java API. Once the blueprint is added to the catalog, the use of Java will be entirely hidden
  from users of that blueprint.

The Apache Brooklyn community is striving to make YAML-based blueprints as simple as possible -
if you come across a use-case that is hard to do in YAML then please let the community know.

