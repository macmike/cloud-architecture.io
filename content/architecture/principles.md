+++
title = "Principles"
date = 2019-03-27T11:02:38Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = "200"

[menu.main] 
    Name = "Principles" 
    identifier = "principles"
    parent = "architecture"
+++

Having a common understanding of architecture, regardless of the format of that understanding (documents, models, sketches, whiteboards, implicit team knowledge), is described as "Intentional Architecture"..

**Good** Architecture and design have the folliowing characteristics:

* Intentional structure and behavior
* Highly modular: consisting of separate services with well-designed APIs
    * Services are highly cohesive
    * Services are loosely coupled
    * Services have low algorithmic complexity
* Avoids duplication
* Well described Services: modular elements have simple expressive meaningful names enabling readers to quickly understand their purpose
* Runs and passes all defined tests or acceptance criteria
* Lightweight documentation
* Use Infrastructure-as-Code

Some additional Cloud Architecture Principles that are often useful:

* Use Serverless event-driven architectures first, drop to PaaS if required, and IaaS of strictly necessary
* Seperate Compute and Storage
* Express Services as APIs using ubiquitous standards (HTTPS REST + JSON)
* Use Managed Services where possible rather than inventing your own
* Use Immutable Infrastructure - rebuild the infrastructure when you deploy, instead of editing what's running on existing infrastructure
* Don't SSH or exec in, build new
* Prove, don't guess

