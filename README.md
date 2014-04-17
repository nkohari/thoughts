# Definitions

- *concern* - a solution for a problem that must be solved by the system
- *object* - a piece of code which implements one or more concerns
- *class* - the manner in which an object is implemented (its blueprint)
- *type* - the manner in which an object can communicate with other objects (its interface)
- *factory* - the manner in which objects are created (typically by calling a class's constructor)
- *lifecycle* - a rule that determines when objects are created and destroyed
- *component* - the fusion of a factory, a type, and a lifecycle, assigned a unique name in a system
- *binding* - the metadata that describes a component (its blueprint)
- *dependency* - a unidirectional link between a component and another component
- *instance* - an object that represents an occurance of a component
- *resolution* - the act of retrieving an instance
- *conditional resolution* - where different dependencies might be resolved depending on context
- *container* - the piece of code that, given a component's name, uses bindings to resolve the component

# Typical Lifecycles

- *transient* - a new instance will be resolved on each request
- *singleton* - only one instance will be created, and subsequent requests will resolve the same instance
- *pooled* - up to N instances will be resolved, and each request will block until an instance is available
- *scoped* - a new instance will be resolved for each new context (thread, request, etc.), but subsequent
  requests within the same context will return the same instance

# Notes

1. The most common component structure just contains a class and a lifecycle. The class's type
   is used as the type of the component, and the class's constructor is used as the component's factory.
2. Classes that implement components should typically be stateless, except for dependencies that are
   resolved by the container, and real external state (file handles, network connections, etc.)
3. Because state is irrelevant, a system often has no need to create multiple instances of a component.
   As a result, the most components have a singleton lifecycle.
4. Each component should only implement a single concern. If additional concerns are necessary
   to solve a concern, additional components should be defined and declared as dependencies.
5. Resolved dependencies should be treated as immutable. Once an instance has been provided
   a reference to another instance, it should not be be altered to point at a different instance.
6. When a component A has a dependency on a component B, a different instance of component B may
   fulfill the dependency for each instance of component A.
