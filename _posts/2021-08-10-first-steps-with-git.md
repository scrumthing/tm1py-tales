---
layout: post
title:  "First Steps with the GIT-integration"
date:   2021-08-10 9:43:27
categories: personal-story
---

Maybe you have heard of the 

We all have been there. Nobody is supposed to change something in production until someone did. Either by accident or on purpose. The WHY does not matter when the server is down. If you want to quickly figure out what is broken, you have to find out what changed. 



If you are lucky, you have not only access to one of those tools but are also an admin user. Then you can create your own TurboIntegrator process which exports a subsection of the cube via `ASCIIOutput` into a text file. Hopefully it does not mix up the decimal separator and the column delimiter is not used in an element name. But otherwise you will be fine and the best part is: You can schedule it. But you still end up with a text file.  
If you are not an admin, you could still rely on that but always need an admin to change your export settings. That gets especially annoying when you change something in your analysis code and then have to match that change with the export and have to wait on someone to change it.

Manual Way
=====


Simplify with GIT
=====



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