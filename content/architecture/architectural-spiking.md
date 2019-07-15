+++
title = "Architectural Spiking"
date = 2019-03-27T11:03:08Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 600

[menu.main] 
    Name = "Spiking" 
    identifier = "architectural-spiking"
    parent = "architecture"
+++

>Architectural Spiking is running a small technical experiment, building working software to prove or disprove feasibility or a specific hypothesis. Spikes are throw away code they are not integrated into released Products, they are used to prove or disprove a theory.

Spiking is intended to investigate an area, reduce complexity, mitigate a risk or otherwise prove/disprove a theory. By diving deep into the solution space (a vertical “spike”) we can understand whether our early architectural ideas are likely to work. Spikes are particularly useful during [Architectural Synthesis]({{< ref "architectural-synthesis.md" >}}). 
 
The purpose of a spike is to test a theory, not to create part of a working product. So although they are built as working software, they are throw-away code, usually ignoring all architectural, style and even good coding guidelines in favor of expediency. Spiking is an excellent form of risk mitigation, and a great way to reduce [Complexity]({{< ref "complexity.md" >}}) through learning.
 
We recommend that Spikes are formed by articulating a theory and a simple test or two. Although we describe Spikes as “throw-away code” we don’t actually throw them away. We don’t integrate them into our real code but they are useful to keep, alongside their specification/tests for people to refer to later or find out how something was done.
 
Here’s a simplistic example of a real spike for a system that was looking to access a SQL Server database using JavaScript. If this spike failed the team had other ideas, but this was a feasibility test they needed to answer.
{{< figure src="/images/architectural_spike.png" alt="Architectural Spike" class="img-800-center">}}

 This was the entire documentation for a Spike. The spike involved doing some web searching, running some command lines and writing around 5 lines of code for each theory, which proved both cases. The team simply ticked the tests and saved the following produced assets:

* Spike documentation
* Links to online guidance
* Install scripts
* Produced code

The team were then able to reduce a risk related to technical integration (although had to create some new risks around the security implications of accessing a database using local Javascript – but that’s a different story).
 