# Slawek's reading-list
Interesting blog posts and articles I've encountered, grouped by month. Mostly about tech.


## 2021/April
- [Dex: array programming with typed indices, workshop paper](https://openreview.net/pdf?id=rJxd7vsWPS)
  - DeepMind experiments with more functional approach to array programming, where array shapes are checked in compile time (type safety achieved with dependent types)
  - FP combines well with parallel execution (compilation to parallel env)
  - github repo: https://github.com/google-research/dex-lang
  - (still need to read it) full-paper published recently: [Getting to the Point. Index Sets and Parallelism-Preserving Autodiff for Pointful Array Programming](https://arxiv.org/pdf/2104.05372.pdf)
  - fun fact: at the moment A. Paszke is the first paper author and the second GH contributor
- [What worries me about AI, F.Chollet](https://medium.com/@francois.chollet/what-worries-me-about-ai-ed9df072b704)
  - Article theme reminds me Social Dilemma, i.e. intelligence explosion is bonkers and we should be more worried about AI integrated with social networks that learns to manipulate human behavior.
  - Francois touches on inspiring point - what if newsfeed objective functions have been put into control of users themselves - imagine personal assistant that knows your psychological profile, it read all of the books, knows millions of other people and you can explicitly ask it to expand your knowledge to become an expert in the chosen set of topics and it also would help you control time spent on the platform.
- [An introduction to property based testing](https://fsharpforfunandprofit.com/pbt/) - slides from the presentation
  - Illustration of how well formulated properties can determine the correct implementation of the software under test.
  - Especially useful bit was about patterns helpful in coming up with good and powerful properties:
    - "different paths, same destination", "there and back again", "some things never change, i.e. finding invariants", exploiting idempotence, "solve smaller problem first", "hard to prove, easy to verify", "the test oracle",
  - [The conference talk](https://vimeo.com/68383317) linked at the end had nice examples of leveraging PBT in practice in distributed systems. My main takeaway was that very complex systems can be modelled with a simpler in-memory implementation that captures intention of the system on a different level of abstraction and sometimes modelling only a small subset of real functionalities combined with PBT already allows to surface **a lot** of bugs. It's also the most sane strategy to debug complex concurrency issues. 
- [Six approaches to dependency injection](https://fsharpforfunandprofit.com/posts/dependencies/)
  - Quite informative overview. By dependency author means piece of code with either side-effects or logic that may be dynamically swapped in the runtime (strategy pattern).
  - Personally, I disagree with this article on two things:
    - Comparing OOP-style dependency injection to the Reader monad is incorrect. In my view OOP-style DI is simply [dependency parameterization](https://fsharpforfunandprofit.com/posts/dependencies-2/), i.e. passing dependencies via class constructors is equivalent to using partially applied functions. Mark Seemann in [Partial application is dependency injection](https://blog.ploeh.dk/2017/01/30/partial-application-is-dependency-injection/) seems to share the same view as me.
    - There is a claim that composing pure and impure function will not result in the impure output function. In my opinion that's obviously false, composed function will produce side-effects and that's a basic reason why IO monad in Haskell type system is very "contagious". Similar opinion is again expressed by Mark Seeman in [the aforementioned blog post](https://blog.ploeh.dk/2017/01/30/partial-application-is-dependency-injection/).
  - The Free monad interpreter pattern as way of avoiding side-effects seems to me a bit over-engineered for the real-world applications, especially if one thinks about handling logging this way (which technically is a side-effect).
- [Data, objects, and how we're railroaded into poor design](https://www.tedinski.com/2018/01/23/data-objects-and-being-railroaded-into-misdesign.html)
  - Programs can be modeled with two pieces: data i.e. immutable values with exposed fixed schema and objects - sets of operations around encapsulated state. Author thinks it's critical to properly distinguish the two and argues that programming languages rarely support both of them well, often falling into the extremes (Haskell encourages to build around data, when in Java almost everything is an object).
- [Expression Problem](https://wiki.c2.com/?ExpressionProblem)
  - Defining an interface (fixed set of operations), makes it easy to add new type variants without breaking the clients. The opposite is true for a fixed set of type variants, a.k.a. sum type - it's easy to add new operations (just create a new function and pattern match over type variants), but adding new type would break other clients which already used that union type.
  - The interface approach dominates in OOP languages, whereas FP embraces algebraic data types.
  - In the light of above, it's less surprising that FP languages are more often used in applications with fixed data types (e.g. compilers) and OOP fits better web apps where underlying data changes more often. However, I imagine mix of both working quite well (what resonates with [Data, objects, and how we're railroaded into poor design](https://www.tedinski.com/2018/01/23/data-objects-and-being-railroaded-into-misdesign.html)).
  - Importantly, sum type can be simulated in Java with a visitor pattern!
  - There are constructs that solve that "problem" (e.g. type classes), but solving it may be not worth it, as pointed out in the article below.
- [Design duality and the expression problem](https://www.tedinski.com/2018/02/27/the-expression-problem.html)
  - I really liked the analogy to math, where natural numbers are more data oriented (definition specifies fixed data upfront) and more operations are added on top, whereas abstract algebra (groups, rings etc) defines fixed operations and finds structures implementing them (types).
  - Important one: client extensibility should not be a default mode, as closing operations and types extension makes it possible to add new things from designer POV (without breaking the clients)
- [Designing abstractions with properties in mind](https://www.tedinski.com/2018/04/24/design-and-property-tests.html)
  - Property testing seems powerful - once you define one against the abstraction (e.g interface) you can test all implementations the same way.
- [A quick tour of generic-random](https://blog.poisson.chat/posts/2018-01-05-generic-random-tour.html)
  - Very cool library for saving a lot of boilerplate in Haskell when testing code with custom algebraic data types and QuickCheck.  
- Book: Java Concurrency in Practice (in progress)
  - Key topics: compound actions, visibility (thread caches etc), encapsulation helps in thread safety, without synchronization Java may change operation order, safe publication, confinement (thread, instance, stack), trade-off between synchronization and performance, different ways of achieving thread safety (e.g. immutability), documenting and being aware of concurrency policies
- [Perceiver: General Perception with Iterative Attention](https://arxiv.org/abs/2103.03206)
  - Multiple approaches have been tried to mitigate attention O(n^2) time and memory complexity, but apparently asymetric attention with latent array makes it work quite well? 
  - Attention maps from cross-attention layers don't look that convincing to me.
  - Transformer based NN architecture goes multi-modal, quite impressive. Wondering if the path forward is about less architectural bias and even more training data.
