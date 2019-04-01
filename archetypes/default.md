+++
title = "{{ replace .Name "-" " " | title }}"
date = {{ .Date }}
draft = false
tags = ["tag1","tag2"]
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 100


[menu.main] 
    Name = "{{ replace .Name "-" " " | title }}" 
    identifier = "{{ replace .Name "-" " " | title }}"
    parent = "section"
+++