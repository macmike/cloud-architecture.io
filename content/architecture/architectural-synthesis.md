+++
title = "Architectual Synthesis"
date = 2019-03-27T11:04:12Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 350


[menu.main] 
    Name = "Synthesis" 
    identifier = "architectual-synthesis"
    parent = "architecture"
+++


[Complexity]({{< ref "complexity.md" >}}) can occur in different areas of a problem, and requires different architectural approaches to simple problems.

>Architectural Synthesis is the creative problem solving activity that turns a set of requirements or direction into an early candidate architecture identifying a possible solution.

The “magic sauce” in software design, **architectural synthesis** is the activity that shapes initial candidate architecture. Based on user needs, requirements (which will have little detail but hopefully represent scope), and investigation into non-functional needs an Architect or team will come up with a number of options for how to meet the needs, or solve the problem. Architectural synthesis is dependant on the complexity of the problem being addresed:
 
* For **simple** pieces of work, architectural synthesis is implicit as the answer is already obvious to everyone.
* For **complicated** pieces of work, investigation into where areas of complication are (using an Architectural Profile) backed up with experience and experimentation/spiking tend to lead pretty quickly to a candidate architecture.
* For **complex** work we recommend a series of experiments/spikes to investigate areas of complexity or try ideas that might work towards delivering business value. If possible, measurement of emergent outcomes will allow multiple candidate architectures to be compared against each other.
 
Architectural synthesis is a creative process, especially when dealing with anything other than simple work. It is often the point where the level of complexity will be recognized. Investigations and spiking will often change understanding of complexity and risks, either uncovering them or addressing them. 
 
We do not recommend following a standard process for synthesis since it’s essentially creative idea generation, and it should not be rushed. In our experience critical thinking and logical analysis can help architectural synthesis.

Cloud is a great enabler for dealing with complicated and complex architectural synthesis since it allows different ideas to be tried, quickly and monitors for cost, performance and stability. Being able to rapidly change architectures through Infrastructure-as-Code reduces the cost of architectural experimentation, or going down a few dead ends while exploring a problem.

