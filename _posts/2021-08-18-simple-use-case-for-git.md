---
layout: post
title:  "Simple Use Case for GIT"
date:   2021-08-18 9:43:27
categories: personal-story
---

What is the GIT-integration?
=====
Maybe you have heard of the new GIT-integration in TM1. It allows you to do version control with your TM1 model. You can track changes in a database or use it to migrate objects between databases. It allows for a DevOp-approach to TM1 where you automatically run integration tests before you move an object like a process or cube from development to production.  
It brings a huge potential to TM1 but lacks frontends to easily use it at the moment. TM1py on the other hand allows you to use the GIT-integration. Here is a simple use case to get you started with GIT while at the same time allows you to continue as before. 


Automatically Track Changes via GIT
=====

We all have been there. Nobody is supposed to change something in production until someone did. Either by accident or on purpose. It always happens and some of those times it breaks things and you have to figure out which changes was the source of the problem. 

There are no easy ways to figure that out. You could look for comments and documentation but that would be getting lucky and in our job we never get lucky. You could check for modification date on certain files but that is although not very reliable. There are third party tools which help you with that but for a price. 

In comes TM1py and the new GIT-functionality added in v 1.7. It allows you to initialize GIT, push and pull or simply request the status of the GIT-connection. (For information on how to set up GIT in your TM1 database, please check [Yuris blog](https://www.ykud.com/blog/cognos/tm1-cognos/git-integration-for-tm1-part-1/). He described it very well.)

The following example simply pushes all TM1 objects into a GIT-repository. It could be used in a daily job to track changes of the system over time. Note that it is meant as a simple way to quickly check changes to your system. It does not track who changed what, etc. For that you have to dive deeper into the GIT-integration. 

``` python
from TM1py import TM1Service

# change for your TM1 system
with TM1Service(address='localhost', port=12354, ssl=True, user='admin', password='apple') as tm1:
    # Add your parameters here
    git_config_push = {
        'username':'john.doe',
        'password': 'a1s2d3f4g5',
        'author': 'John Doe',
        'email': 'john.doe@123.com',
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