---
layout: post
title:  "First Steps with the GIT-integration"
date:   2021-08-10 9:43:27
categories: personal-story
---

Maybe you have heard of the new GIT-integration in TM1. 

We all have been there. Nobody is supposed to change something in production until someone did. Either by accident or on purpose. The WHY does not matter when the server is down. If you want to quickly figure out what is broken, you have to find out what changed. 


Manual Way
=====

Manual labor is so boring. 

Simplify with GIT
=====

You do not have to get into all the details of the GIT integration of TM1. 

``` python
from TM1py import TM1Service

with TM1Service(address='localhost', port=12354, ssl=True, user='admin', password='apple') as tm1:
    git_config_push = {
        'username':'john.doe',
        'password': 'a1s2d3f4g5',
        'author': 'John Doe',
        'email': 'john.doe@123.com',
        'git_url': 'https:GITURL',
        'deployment': 'production',
        'branch': 'prod',
        'execute': 'True',
        'message': 'Daily Check for uncomitted Changes' 
    }

    try:
        push_status = tm1.git.git_push(git_config_push)
        print(push_status.text)

    except Exception as e:
        print(e)

```


_____

Written by [![GitHub](https://i.stack.imgur.com/tskMh.png) Christoph Hein](https://github.com/scrumthing)