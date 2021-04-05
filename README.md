# Slawek's reading-list
Interesting articles I've encountered grouped by month. Mostly about tech.


## 2021/April
- [Data, objects, and how we're railroaded into poor design](https://www.tedinski.com/2018/01/23/data-objects-and-being-railroaded-into-misdesign.html)
  - Programs can be modeled with two pieces: data i.e. immutable values with exposed fixed schema and objects - sets of operations around encapsulated state. Author thinks it's critical to properly distinguish the two and argues that programming languages rarely support both of them well, often falling into the extremes (Haskell encourages to build around data, when in Java almost everything is an object).
- [Expression Problem](https://wiki.c2.com/?ExpressionProblem)
  - Defining an interface (fixed set of operations), makes it easy to add new type variants without breaking the clients. The opposite is true for a fixed set of type variants, a.k.a. sum type - it's easy to add new operations (just create a new function and pattern match over type variants), but adding new type would break other clients which already used that union type.
  - The interface approach dominates in OOP languages, whereas FP embraces algebraic data types.
  - In the light of above, it's less surprising that FP languages are more often used in applications with fixed data types as compilers and OOP fits better web apps where underlying data changes more often. However, I imagine mix of both working quite well (what resonates with [Data, objects, and how we're railroaded into poor design](https://www.tedinski.com/2018/01/23/data-objects-and-being-railroaded-into-misdesign.html)).
  - Importantly, sum type can be simulated in Java with a visitor pattern!
  - There are constructs that solve that "problem" (e.g. type classes), but solving it may be not worth it, as pointed out in the article below.
- [Design duality and the expression problem](https://www.tedinski.com/2018/02/27/the-expression-problem.html)
  - I really liked the analogy to math, where natural numbers are more data oriented (definition specifies fixed data upfront) and more operations are added on top, whereas abstract algebra (groups, rings etc) define fixed operations and find structures implementing them (types).
  - Important one: client extensibility should not be a default, as closing operations and types extension makes it possible to add new things from designer POV (without breaking the clients)
- [Designing abstractions with properties in mind](https://www.tedinski.com/2018/04/24/design-and-property-tests.html)
  - Property testing seems powerful - once you define one against the abstraction (e.g interface) you can test all implementations the same way.
- [A quick tour of generic-random](https://blog.poisson.chat/posts/2018-01-05-generic-random-tour.html)
  - Very cool library for saving a lot of boilerplate in Haskell when testing code with custom algebraic data types and QuickCheck.  
- Book: Java Concurrency in Practice (in progress)
  - Key topics: compound actions, visibility (thread caches etc), encapsulation helps in thread safety, without synchronization Java may change operation order, safe publication, confinement (thread, instance, stack), trade-off between synchronization and performance, different ways of achieving thread safety (e.g. immutability), documenting and being aware of concurrency policies
- [Perceiver: General Perception with Iterative Attention](https://arxiv.org/abs/2103.03206)
  - Multiple approaches have been tried to mitigate attention O(n^2) time and memory complexity, but apparently asymetric attention with latent array makes it work quite well? 
  - Attention maps from cross-attention layers don't look that convincing to me.
  - Transformer based NN architecture goes multi-modal, quite impressive. Wondering if the path forward is about less architectural bias and even more data.
