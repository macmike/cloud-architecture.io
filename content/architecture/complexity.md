+++
title = "Complexity"
date = 2019-03-27T11:04:12Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 300


[menu.main] 
    Name = "Complexity" 
    identifier = "complexity"
    parent = "architecture"
+++


>Any problem or piece of work can be considered in terms of its complexity. Problems can be simple, complicated or complex. 

Different types of problems require different types of solutions, and not every approach is suitable for every type of problem. Complexity is one of the most significant factors. Many organizations will have work at multiple levels of complexity as part of their portfolio, and often treat all of them in the same way, incorrectly applying the same processes without considering how they may be inappropriate. 
 
**Simple** work is that which is well understood. Risk is low because we understand the problem and the solution is obvious to everyone involved. In these cases, traditional forward planning and management with a focus on reducing variability to improve efficiency can work well, as long as there is rapid enough feedback to deal with disruptive change. **Continuous flow** models and/or service management are well suited to this work.
 
**Complicated** work requires analysis to understand the connections between cause and effect, or required inputs and outputs. Investigation and some creative thinking is necessary to understand a problem and then propose a solution. **Agile/Iterative** models are well suited to this work. Complicated endeavors are built upon specialist knowledge and aren't just obvious. They might take a lot of time and skill to do but are ultimately predictable processes. For example, a recursive sorting algorithm in computer programming is complicated, it involves variables, loops and recursion - it’s not easy for everyone to understand but it’s very predictable. Building a car engine is complicated.
 
**Complex** work involves many inter-dependent integrating parts that interact in a number of ways resulting in unpredictable, emergent outcomes. The relationship between cause and effect isn’t predictable, undermining planning, estimation as well as analysis and design practices. **Organic networks, outcome orientated teams** and high complexity architecture practices are used for this kind of work. Complex endeavors are those which have many influencing parts and events whose interactions are not predictable. Driving a car is complex.
 
**Complicated is easy if you can get the right skills lined up. Complex is always hard.**


#### High-Complexity Architecture


>High complexity architecture involves applying architecture practices and principles to business and technical problems involving many interdependent integrating parts that interact in a number of ways resulting in unpredictable, emergent outcomes.

Most organizations work with complicated problems, not high complexity issues. However, to innovate or invent ahead of competitors or adversaries, organizations often have to work in higher complexity areas. When working on very new ideas, or new problem spaces, there can be a lack of knowledge and tried and tested techniques; this widens the cone of uncertainty significantly. Where there are a large number of interacting parts and a large number of interactions complexity can be very high.
 
Very high complexity architectures are those in which a number, or all, of the following conditions are true:

* There is extensive integration between many independent components, technologies
* The work is highly speculative and unpredictable, we expect to fail fast and often
* There isn’t a large amount of domain knowledge or experience in the field
* One or more of the dimensions of an [architectural profile]({{< ref "architectural-profiling.md" >}}) are “Very high”
* Estimates are extremely uncertain
* Risks are very high
* Extremely large scale (of data, change and distribution)
* There is a complex logical relationship between inputs and emergent properties or behaviors

Part of the job of architecture is to reduce complexity. When working in high complexity systems, the intent is often more important than the detail. Work is often highly speculative as people are inventing new techniques that may or may not work. Empirical feedback becomes more useful than specification, and due to the experimental “sensing” nature of high complexity work details will change significantly. Failure is always likely in high-complexity work and so management practices that assume success will fail to cope with complexity. Complexity cannot be controlled, it can only be responded to. The following practices fail or are extremely dysfunctional for high-complexity problems:

* **forward planning** - We don’t yet know how we’re going to solve the problem, if we even can. Plans will change quicker than they can be written down. “Probing and sensing” is more appropriate.
* **detailing requirements** -  The intent is important, not the detail of how. Our technical solutions are likely to change significantly meaning that details will change. A sub-optimal solution might be the only cost-effective option significantly affecting scope.
* **analysis and design** - Decomposing problems into manageable chunks isn’t the right answer when the complexity is in the number of “chunks” and their interactions. Instead we need to manage emergent properties and create architectural experiments ([spikes]({{< ref "architectural-spiking.md">}})) to prove or disprove our ideas.
* **user-centric design** - Users are unlikely to have resolved the high complexity issues and may not even understand the problem fully. Giving the users what they want, often a good idea, is often the opposite of a high complexity solution. Users seek simplicity, and although this is a good idea in terms of interaction with high complexity architecture, designing interaction doesn’t help solve the problem. Since scope and technology are likely to change, UX detail is best left until the solution is more stable.
* **estimation** -  By the nature of the complexity estimations will all be extremely uncertain. Numbers may be significant orders of magnitude out. Instead organizations are better off funding experimentation in a number of timeboxes to see how much complexity can be produced in those timeboxes through spiking and experiments.


When working with high complexity architecture, standard Enterprise Architecture (if it exists) may need to be abandoned to deal with emergent behavior. However, the cost of not using Enterprise Architecture should not be considered as an inhibitor to high complexity work if the business opportunity is significant enough.
 
In Solution (multi-system) Architecture for high complexity architectures, a common dysfunction is to try and connect all of the architectural information and system architectures. We’ve seen organizations create massive over-complicated models that try and resolve integration complexity by documenting it all. Well-meaning, but ineffective and wasteful. This approach is counter-productive because the complexity comes not from the number of items, but the dynamism of their interactions and unpredictable aggregate behavior. These large models are, at best, a snapshot view of complexity at a single point in time but they don’t help anyone solve the problems. 
 
Instead, when working with high complexity Solution and System Architectures we recommend architecting for change, not solution requirements. By that we mean that since requirements, scope and emergent behavior are so likely to change the only thing we really know the architecture needs to support is change. Therefore, focus on the principle, technology and mechanisms that enable change such as: 

* High cohesion, low coupling principles
* Integration architecture (message passing, queueing, elastic deployment, discovery, data formats
* The, relatively simpler, complicated parts
* Possible reduction in complexity through low algorithmic complexity, refactoring out components, heuristic approaches
* Use of serverless/event-driven architectures to facilitate changing approach
* Focus on data flow, not structure of services
* Use cloud managed services to reduce complexity and infrastructure management wherever possible to allow more effort to be spent on the business problem

Since the behavior and properties of high complexity systems are emergent we recommend creating a “pull” towards Business Value through rapid, preferably continuous, integration and deployment. Creating measures that reflect desired outcomes (not intermediary stages or logical decomposition) and test every change in terms of moving towards or away from “good” emergent behavior. 
 
At the extreme end of this high complexity scale, using machine learning and evolutionary techniques to generate possible solutions and test for emergent properties can be useful to speed up iteration cycles. 