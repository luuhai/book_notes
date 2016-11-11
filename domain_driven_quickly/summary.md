###1. What is Domain-Driven Design
* Software development is most often applied to automating processes that exist in the real world, or providing solutions to real business problems. The business processes being automated or real world problems are the domain of the software.
* When we begin a software project, we should focus on the domain it is operating in. The entire purpose of the software is to enhance a specific domain so it has to fit harmoniously with the domain it has been created for, otherwise it will introduce strain into the domain, provoking malfunction, damage... The best way to do it is to make software a reflection of the domain. Software has to model the domain.
* We need to create an abstract of the domain. The raw knowledge about domain is not going to be easily transformed into software constructs, unless we build an abstraction of it, a blueprint in our minds. What is this abstraction? It is a model of the domain. A domain model is not a particular diagram; it is the idea that the diagram is intended to convey. It is not just the knowledge in a domain expert's head; it is a rigorously organized and selective abstraction of that knowledge.
* The model is our internal representation of the target domain, and it is very necessary throughout the design and the development process. We need to organize information, to systematize it, to divide it up in smaller pieces, to group those pieces into logical modules, and take one at a time and deal with it. We even need to leave some parts of the domain out.
* We need model in order to be able to deal with complexity. We need to communicate this model with domain experts, with fellow designers, and with developers.
* When we have a model expressed, we can start doing code design, which is different from software design. Here code design patterns come handy, and they should be applied when necessary.
* There are different approached to software design. The traditional approach is `waterfall` design method. The main problem with it is that there is no feedback from the analysts to the business experts or from the developer to the analysts. Another approach is the `Agile` methodologies. These methodologies are a collective movement against the `waterfall` approach. They employ a great deal of implementation flexibility, and through iterative development with continuous business stakeholder participation and a lot of refactoring, the development team gets to learn more about the customer domain.

**Building Domain Knowledge**

  + You need to learn as much as possible about the domain from the experts. And by putting right questions, and processing the information in the right way, you and the experts will start to sketch a view of the domain, a domain model.
  + The communication is not one way, from domain experts to the software architecture and further to developers. There is also feedback, which helps create a better model, and a clearer and more correct understanding of the domain.

###2. The Ubiquitous Language
* A core principle of domain-driven design is to use a language based on the model. Since the model is the common ground, it is appropriate to use it as the building ground for this language. It is called the `Ubiquitous Language`.
* The `Ubiquitous Language` connects all the parts of the design, and creates the premise for the design team to function well. Languages do not appear overnight. We need to find key concepts which define the domain and the design, and find corresponding words for them, and start using them. Iron out difficulties by experimenting with alternative expressions, which reflect alternative models. Then refactor the code, renaming classes, methods, and modules to conform to the new model. Resolve confusion over terms in conversation, in just the way we come to agree on the meaning of ordinary words. Building a language like that has a clear outcome: the model and the language are strongly interconnected with one another.
* It is also highly recommended for the developers to implement the main concepts of the model in the code. By creating classes for the corresponding model concepts, the language and the code. Having the code express the model pays off later in the project, when the model grows large, and when changes in the code can have undesireable consequences if the code was not properly designed.
* There are many ways to communicate during design, such as using `UML` diagram, writing documents with small diagrams or using code...

###3. Model-Driven Design

**Entities**

  + There is a category of objects which seem to have an identity, which remain the same throughout the states of the software. For these objects it is not the attributes which matter, but a thread of continuity and identity, which spans the life of a system and can extend beyond it. Such objects are called `Entities`.
  + OOP objects have a reference of a memory address for each object, this reference is nunique for each object at a given moment of time, but it will not stay so for an indefinite period of time, so it is not the identity we are talking about. These objects are not entities.
  + Mistaken identity can lead to data corruption. It is importang for two objects with different identities to be easily distinguished by the system, and two objects with the same identity to be considered the same by the system. If that condition is not met, then the entire system can become corrupted.
  + Implementing entities in software means creating identity. Usually the idenity is either an attribute of the object, a combination of attributes, an attribute specially created to preserve and express identity, or even a behavior.
  + `Entities` are important objects of a domain model, and they should be considered from the beginning of the modeling process. It is also important to determine if an object needs to be an entity or not.

**Value Objects**

  + Tracking and creating identity comes with a cost. It is difficult and takes a lot of careful thinking to decide what makes an identity. There are also performance issue.
  + There are cases when we need to contain some attributes of a domain element. We are not interested in which object it is, but what attribute it has. An object that is used to describe sertain aspects of a domain, and which does not have identity, is named `Value Object`.
  + It is necessary to distinguish between `Entity Objects` and `Value Objects`. It is recommended to select as entities only those objects which conform to the entity definition, and make the rest of the objects `Value Objects`.
  + It is highly recommended that value objects be immutable. Being immutable, and having no identity, `Value Objects` can be shared. Immutable objects are sharable with important performance implications. They also manifest integrity, i.e. data integrity. If there is no identity, you can make as many copies as you wish, and destroy all of them when necessary.
  + `Values Objects` can contain other `Value Objects`, and they can even contain references to `Entities`. Attributes chosen to make up a `Value Object` should form a conceptual whole.

**Services**

  + There are some actions in the domain which do not seem to belongs to any object. They represent an important behavior of the domain, so they can not be neglected or simply incorporated into some of the `Entities` or `Value Objects`. Adding such behavior to an object wuold spoil the object, making it stand for functionality which does not belong to it. Often this kind of behavior functions across several objects, perhaps of different classes.
  + When such a behavior is recognized in the domain, the best practice is to declare it as a `Service`. Such an object doas not have an internal state, and its purpose is to simply provide functionality for the domain. It is much better to declare the `Service` explicitly, because it creates a clear distinction in the domain, it encapsulates a concept.
  + `Services` act as interfaces which provide operations. A `Service` is not about the object performing the service, but is related to the objects the operations are performed on/form, so it usually becomes a point of connection for many objects. This is one of the reasons why behavior which naturally belongs to a `Service` should not be included into domain objects, or else it will cause a high degree of coupling between many objects, which is a sign of poor design.
  + A `Service` should not replace the operation which normally belongs on domain objects. But when such an operation stands out as an important concept in the domain, a `Service` should be created for it. There are three characteristics of a `Service`:

    1. The operation performed by the `Service` refers to a domain concept which does not naturally belong to an `Entity` or `Value Object`.
    2. The operation performed refers to other objects in the domain.
    3. The operation is stateless.

  + While using `Services`, it is important to keep the domain layer isolated. It is easy to get confused between services which belong to the domain layer, and those belonging to the infrastructure. There can also be services in the application layer which adds a supplementary level of complexity.
  + Both application and domain `Services` are usually built on top of domain `Entities` and `Values` providing required functionality directly related to those objects. If the operation performed conceptually belongs to the application layer, then the `Service` should be placed there. If the operation is about domain need, then it should belongs to the domain layer.

**Modules**

  + For a large and complex application, the model tends to grow bigger and bigger. The model reaches a point where it is hard to talk about as a whole, and understanding the relationships and interactions between different parts becomes difficult. For that reason, `Modules` are used as a method of organizing related concepts and tasks in order to reduce complexity.
  + It is easier to get the picture of a large model if you look at the modules it contains, then at the relationships between those modules. After that one can start figuring out the details inside of a module.
  + Software code should have a high level of cohesion and a low level of coupling. It is recommended to group highly related classes into modules to provide maximum cohesion possible. Two of the most used types of cohesion are `communicaional cohesion` and `functional cohesion`. Communcational cohesion is achieved when parts of the module operate on the same data. The functional cohesion is achieved when all parts of the module work together to perform a well-defined task. This is considered the best type of cohesion.
  + Modules should have well defined interfaces which are accessed by other modules. Instead of calling three objects of a module, it is better to access one interface, because it reduces coupling. Low coupling reduces complexity, and increases mantainability.
  + Give the `Modules` names that become part of the `Ubiquitous Language`. `Modules` and their names should reflect insight into the domain.
  + After the role of the module is decided, it usually stays unchanged, while the internals of the module may change a lot. It is recommended to have some flexibility, and allow the modules to evolve with the project, and should not be kept frozen.

**Aggregates**

  + `Aggregate` is a domain pattern used to define object ownership and boundaries.
  + A model can contain a large number of domain objects. It happens that many objects are associated with one another, creating a complex net of relationships. The challenges of models are most often not to make them complete enough, but rather to make them as simple and understandable as possible. Most of the time it pays of to eliminate or simplify relations from the model. It is difficult to guarantee the consistency of changes to objects in a model with complex associations.
  + Therefore, use `Aggregates`. An `Aggragate` is a group of associated objects which are considered as one unit with regard to data changes. The `Aggregate` is demarcated by a boundary which separates the objects inside from those outside. Each `Aggregate` has one root. The root is an `Entity`, and it is the only object accessible from outside. The root can hold references to any of the aggregate objects, and the other objects can hold references to each other, but an outside object can hold references only to the root object.
  + Since other objects can hold references only to the root, it means that they can not directly change the other objects in the aggregate. All operations are contained inside the aggregate, and it is controllable. If the root is deleted and removed from memory, all the other objects from the aggregate will be deleted too. It is simple to enforce invariants (which are those rules which have to be maintained whenever data changes) be cause the root will do that.
  + It is possible for the root to pass transient references of internal objects to external ones, with the condition that the external objects do not hold the reference after the operation is finished. One simple way to do that is to pass copies of the `Value Objects` to external objects.
  + If objects of an `Aggregate` are stored in a database, only the root should be obtainable through queries. The other objects should be obtained through traversal associations.
  + Objects inside an `Aggregate` should be allowed to hold references to roots of other `Aggregates`.
  + The root `Entity` has global identity. Internal `Entities` have local identity.

**Factories**

  + `Entities` and `Aggregates` can often be large and too complex to create in the constructor of the root entity. Creation of an object can be a major operation in itself, but complex assembly operations do not fit the responsibility of the created objects. Combining such responsibilities can produce ungainly designs that are hard to understand.
  + `Factories` are used to encapsulate the knowledge necessary for object creation, and they are especially useful to create `Aggregates`. When the root of the `Aggregate` is created, all the objects inside are created with it, and all the invariants are enforced.
  + It is important for the creation process to be atomic. If it is not, there is a chance for the creation process to be half done for some objects, leaving them in an undefined state. This is even more true for `Aggregates`. If an object cannot be created properly, an exception should be raised, making sure that an invalid value is not returned.
  + Therefore, shift the responsibility for creating instances of complex objects and Aggregates to a separates object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create entire `Aggregates` as a unit, enforcing their invariants.
  + A `Factory Method` is an object method which contains and hides knowledge necessary to create another object. To create an object which belongs to an `Aggregate`, the solution is to add a method to the `Aggregate` root, which takes care of the object creation, enforces all invariants, and returns a reference to that object, or to a copy of it.
  + There are times when the construction of an object is more complex, or when the creation of an object involves the creation of a series of objects. Hiding the internal construction can be done in a separate `Factory` object which is dedicated to his task.
  + `Entity Factories` and `Value Object Factories` are different. Values are usually immutable objects, and all the necessary attributes need to be produces at the time of creation. When the object is created, it has to be valid and final. Entities are not immutable. They can be changed later. Another difference comes from the fact that `Entities` need identity, while `Value Objects` do not.
  + There are times when a `Factory` is not needed, and a simple constructor is enough:

    1. The construction is not complicated.
    2. The creation of an object does not involve the creation of others, and all the attributes needed are passed via the constructor.
    3. The client is interested in the implementation, perhaps wants to choose the Strategy used.
    4. The class is the type. There is no hierarchy involved, so no need to choose between a list of concrete implementations.

  + `Factories` need to create new objects from scratch, or required to reconstitute objects which previously existed, but have been probably persisted to a database. Bringing `Entities` back into memory from the database does not need new identities. Also, when a new object if created from scratch, any violation of invariants ends up in an exception. The objects recreated from a database need to be repaired somehow, otherwise there is data loss.

**Repositories**

  + A client needs a practical means of acquiring references to preexisting domain objects. If the infrastructure makes it easy to do so, the developers of the client may add more traversable associations, muddling the model. The overall effect is that the domain focus id lost and the design is compromised.
  + Therefore, use a `Repository`, the purpose of which is to encapsulate all the logic needed to obtain object references.
  + The `Repository` may store references to some of the objects. When an object is created, it may be saved in the `Repository`, and retrieved from there to be used later. If the client requested an object that `Repository` does not have, it may get it from the storage.
  + The `Repository` may also include a `Strategy`. It may access one persistence storage or another based on the specified `Strategy`. It may use different storage locations for different type of objects. The overall effect is that the domain model is decoupled from the need of storing objects or their references, and accessing the underlying persistence infrastructure.
  + Provide methods to add and remove objects, which will encapsulate the actual insertion or removal of data in the data store. Provide methods that select objects based on some criteria and return fully instantiated objects or collecions of objects whose attribute values meet the criteria, thereby sncapsualting the actual storage and query technology. Provide repositories only for `Aggregate` roots that actually need direct access. Keep the client focused on the model, delegating all object storage and access to the `Repositories`.
  + A `Repository` may contain detailed information used to access the infrastructure, but its interface should be simple. A `Repository` should have a set of methods used to retrieve objects. The `Repository` interface may contain methods used to perform some supplementary calculations like the number of objects of a certain type.
  + There is a relationship between `Factory` and `Repository`. While the `Factory` is concerned with the creation of objects, the `Repository` takes care of already existing objects. `Repository` may be seen as a `Factory`, because it creates objects. It is not a creation from scratch, but a reconstitution of an object which existed. We should not mix a `Repository` with a `Factory`. When a new object is to be added to the `Repository`, it should be created first using the `Factory`, and then it should be given to the `Repository` which will store it. `Factories` are pure domain, but `Repositories` can contain links to the infrastructure.

###4. Refactoring Toward Deeper Inside

**Continuous Refactoring**

  + `Refactoring` is the process of redesigning the code to make it better without changing application behavior. Refactoring is usually done in small, controllable steps, with great care so we don't break functionality or introduce some bugs. Automated tests are of great help to ensure that we haven't broken anything.
  + There are refactoring patterns, which represent an automated approach to refactoring. This kind of refactoring, which called technical refactoring, deals more with the code and its quality.
  + There is another type of refactoring, one related to the domain and its model. Every things that is discovered should be included in the design through refactoring. It is very important to have expressive code that is easy to read and understand.
  + Technical refactoring can be organized and structured. Refactoring toward deeper insight cannot be done in the same way, because of the complexity of a model and the variety of models. A good models is the result of deep thinking, insight, experience and flair.
  + All models are lacking depth in the beginning, but we should refactor the model toward deeper and deeper insight.
  + The design has to be flexible. A stiff design resists refactoring.
  + Refactoring can be motivated by an insight into the domain and a corresponding refinement of the model or its expression in code.

**Bring Key Concepts Into Light**

  + Refactoring is done in small steps. There are times when lots of small changes add very little value to the design, and there are times when few changes make a lot of difference. It's a `Breakthrough`.
  + We start with a coarse, shallow model. Then we refine it and the design based on deeper knowledge about the domain. Each refinement adds more clarity to the deisgn. This creates in turn the premises for a `Breakthrough`.
  + A `Breakthrough` often involves a change in thinking, in the way we see the model. It is also a source of great progress in the project, but it also has some drawbacks. A `Breakthrough` may imply a large amount of refactoring, that means time and resources. It is also risky, because ample refactoring may introduce behavioral changes in the application.
  + To reach a `Breakthrough`, we need to make the implicit concepts explicit.
  + The first way to discover implicit concepts is to listen to the language. As we build our `Ubiquitous Language`, the key concepts make their way into it. Sometimes sections of the design may not be so clear. Try to see if there is a missing concept. If one found, make it explicit. Refactor the design to make it simpler and suppler. When building knowledge it is possible to run into contradictions. We should try to reconcile contradictions. Sometimes this brings to light important concepts.
  + Another way of digging out model concepts is to use domain literature. Ther information found in books is valuable, and offers a deep view of the domain.
  + There are other concepts which are very useful when made explicit: `Constraint`, `Process` and `Specification`.

    1. A `Constraint` is a simple way to express an invariant. Placing the `Constraint` into a separate method has the advantage of making it explicit. There is also room for growth adding more login to the methods if the constraint becomes more complex.
    2. `Processes` are usually expressed in code with procedures. The best way to implement processes is to use `Service`. If there are different ways to carry out the process, then we can encapsulate the algorithm in an object and use a `Strategy`. Not all processes should be made explicit. If the `Ubiquitous Language` specifically mentions the respective process, then it is time for an explicit implementation.
    3. A `Specification` is used to test an object to see if it satisfies a certain criteria. The domain layer contains business rules which are applied to `Entities` and `Value Objects`. Some of those rules are just a set of questions whose answer is ""yes" or "no", which can be expressed through a series of logical operations performed on Boolean values, and the final results is also a Boolean. The rule should be encapsulated into an object of ists own, which becomes the `Specification` of the model, and should be kept in the domain layer. Often a single `Specification` checks if a simple rule is satisfied, and then a number of such specifications are combined into one expressing the complex rule.

###5. Preserving Model Integrity

* When multiple teams work on a project, code development is done in parallel, each team being assigned a specific part of the model. It it easy to start form a good mdoel and progress toward an inconsistent one, as nobody takes the time to fully understand the entire model.
* The internal consistency of a model is called `unification`. When the design of the model evolves partially independently, we are facing the possibility to lose model integrity. Preserving the model integrity by striving to maintain one large unified model for the entire enterprise project is not going to work. The solution is we should conciously divide it into several models. Several models well integrated can evolve independently as long as they obey the contract they are cound to. Each model should have a clearly delimited border, and the relationships between models should be defined with precision.

**Bounded Context**

  + Each model has a context. When we deal with a single model, the model is implicit. But when we work on a large enterprise application, we need to define the context for each model we create.
  + A model should be small enough to be assigned to one team. The context of a model is the set of conditions which need to be applied to make sure that the terms used in the model have s specific meaning.
  + The main idea is to defined the scope of a model, to draw up boundaries of its context, then do the most possible to keep the model unified. Explicitly define the context within which a model applies. Explicitly set boundaries in terms of team organization, usage within specific parts of the application, and physical manifestations such as code bases and database schemas. Keep the model strictly consistent within these bounds, but don't be distracted or confused by issues outside.
  + A `Bounded Context` is not a `Module`. A `Bounded Context` provides the logical frame inside of which the model evolves. `Modules` are used to organize the elements of a models, so `Bounded Context` encompasses the `Module`.
  + When different teams have to work on the same model, we have to be aware that changes to the model may break existing functionality. When using multiple models, everybody can work freely on their own piece. Each model can support refactoring much easier, without repercussions on other models. The design can be refined and distilled in order to achieve maximum purity.
  + We need to define the borders and the relationships between different models. This requires extra work and design effort, and there will perhaps some translations between different models.

**Continuous Integration**

  + Even when a team works in a `Bounded Context` there is room for error. If one does not understand the relationships between objects, they may modify the code in such a way that comes in contradiction with the original intent.
  + A model is not fully defined from the beginning. It evolves continuously based on new insight in the domain and feedback from the development process. That's why `Continuous Integration` is a necessary process within a `Bounded Context`. We need a process of integration to make sure that all the new elements which are added fit harmoniously into the rest of the model, and are implemented correctly in code. The sooner we merge the code the better. Another necessary requirement is to perform automated tests. The code can be changed to fix the reported errors, because they are caught early, and the merge, build, test process is started again.
  + `Continuous Integration` applies to a `Bounded Context`, it is not used to deal with relationships between neighboting `Contexts`.

**Context Map**

  + While every team works on its model, it is good for everyone to have an idea of the overall picture. A `Context Map` is a document which outlines the different `Bounded Contexts` and the relationships between them.
  + In the end the pieces have to be assembled together, and the entire system must work properly. If the contexts are not clearly defined, it is possible they will overlap each other. If the relationships between contexts are not outlined, there is a chance they won't work when the system is integrated.
  + Each `Bounded Context` should have a name which should be part of the `Ubiquitous Language`. Everyone should know the boundaries of each context and the mapping between contexts and code. A common practice is to define the contexts, then create modules for each context, and use a naming convention to indicate the context each module belongs to.

**Shared Kernel**

  + Uncoordinated teams working on closely related applications my produce results that not fit together. They can spending more on translation layers and retrofitting than they would spend on `Continuous Integration` in the first place, meanwhile duplicating effort and losing the benefits of a common `Ubiquitous Languague`.
  + Therefore, designate some subset of the domain model that the two teams agree to share, includes the subset of code or of the database design associated with that part of model. Integrate a functional system frequently, but less often than the pace of `Continuous Integration` within the teams. During these integrations run the tests of both teams.
  + The purpose of the `Shared Kernel` is to reduce duplication but still keep two separate contexts. If the teams use separate copies of the kernel code, they have to merge the code as soon as possible, at least weekly. A test suite should be in place. Any change of the kernel should be communicated to another team.

**Customer-Supplier**

**Conformist**

**Anticorruption Layer**

**Separate Ways**

  + If we reach the conclusion that integration is more trouble than it is worth, then we should go the `Separate Ways`.
  + The `Separate Ways` pattern addresses the case when an enterprise application can be made up of several smaller applications which have little or nothing in common from a modeling perspective. There is a single set of requirements, and from the user's perspective this is one application, but from a modeling and design point of view it may done using separate models with distinct implementations. If we can divide requirements in two or more sets which do not have much in common, then we can create separate `Bounded Context` and do the modeling independently. That is a minor integration which has to do with organizing the applications, rather than the model behind them.
  + Before going on `Separate Ways` we need to make sure that we won't come back to an integrated system. Models developed independently are very difficult to integrate.

**Open Host Service**

  + When we try to integrate two subsystems, we usually create a translation layer between them. This layer acts as a buffer between the client subsystem and the external subsystem we want to integrate with. If the externam subsystem turns out to be used not by one client, but by several ones, we need to create translation layers for all of them. All those layers will repeat the same task, and will contain similar code
  + The solution is to see the external subsystem as a provider of services. If we can wrap a set of `Services` around it, then all other subsystems will access these `Services` without any translation layer. Define a protocol that gives access to your subsystem as a set of `Services`. Open the protocol so that all who need to integrate with you can use it. Enhance and expand the protocol to handle new integration requirements, except when a single team has idiosyncratic needs. Then, use a one-off translator to augment the protocol for that special case so that the shared protocol can stay simple and coherent.

**Distillation**
