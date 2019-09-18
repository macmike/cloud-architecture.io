+++
title = "IaaS"
date = 2019-03-27T11:07:53Z
draft = false
tags = ["tag1","tag2"]
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 300

[menu.main] 
    Name = "IaaS" 
    identifier = "iaas"
    parent = "cloud"

+++

type

"IaaS" refers to Infrastructure-as-a-Service which is the foundation of cloud computing. IaaS provides compute (VMs), Networking (routes, firewalls, dns) and storage (object stores, databases) over the network created via APIs and usually GUIs.

IaaS enablez the ability to create environments (such as a server configuration) deterministically, based on rules. This means that environment creation becomes predictable, and testable, rather than a variable unknown. 
 
Good IaaS services must be API based to allow development teams to incorporate distribution, load balancing, resilience, fail-over and configuration into the development and build process. Because of the necessary speed, amount of change and quality advantages IaaS provisioning, configuration and tear-down should be automated. 
 
IaaS is sometimes characterized as treating servers as cattle, not pets. They tend not to have special names and designated purposes anymore. Servers are treated as utilities, if one goes wrong we simply turn it off and stand up a new server, with the exact same configuration, in its place.

IaaS is currently best provided by Public Cloud providers rather than built on premises. 