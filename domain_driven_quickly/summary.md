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

###4. Refactoring Toward Deeper Inside

###5. Preserving Model Integrity

