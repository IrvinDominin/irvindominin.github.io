---
layout: post
title: What is Docker?
category: Dev
tags: [Docker]
image: https://irvindominin.github.io/images/WhatIsDocker/docker_logo.jpg
excerpt: "Docker is a wide platform designed to make it simple to create, deploy, and run applications by using containers."
---

Docker is a wide platform designed to make it simple to create, deploy, and run applications by using containers. Containers allow a developer (like me) to package up an application with all of the parts it needs, such as libraries, its dependencies, and the framework itself and ship it all out as one package. So, thanks to the container, the developer can be sure that it's application will run without care on what environment will host the application.

Obviously if the application and the API used are strictly coupled to the OS the application will run only on a compatible host e.g. only on a Windows or Linux machine.

Imagine Docker like a virtual machine. But, the main difference between them, is that Docker instead of creating a whole virtual operating system, allows applications to use the same kernel as the system that they're running on and only requires applications be shipped with things not already running on the host computer. This gives a performance boost and reduces the size of the application.

<div class="post-comparison">
    <div class="post-comparison-left">
        <figure>
            <img class="alignnone size-full wp-image-119" src="/images/WhatIsDocker/VM.png" alt="glfdrio" /> 
            <figcaption>Traditional VM</figcaption>
        </figure>
    </div>
    <div  class="post-comparison-right">
        <figure>
            <img class="alignnone size-full wp-image-119" src="/images/WhatIsDocker/Container.png" alt="glfdrio" /> 
            <figcaption>Container</figcaption>
        </figure>
    </div>
</div>

And VM and Docker can be combined to empower deploying, scaling and managing applications:
<figure>
    <img class="alignnone size-full wp-image-119" src="/images/WhatIsDocker/Together.png" alt="glfdrio" /> 
    <figcaption>Containers and VMs used together</figcaption>
</figure>

<h2>For who Docker is designed?</h2>
The Docker platform is designed to benefit both developers and system administrators, the problematic and well-knowed Dev vs. IT scenario. Using Docker these figures embrace the DevOps (developers + operations) philosophy. 
For developers, it means that they can focus on writing great code without fit the application on the machine that usually in prod is different than in QA. For sysadmins, Docker gives flexibility and potentially reduces the number of machines needed to run applications.

<h2>A container is 1:1 to the machine?</h2>

No! One of the main benefits is that a single Docker can run multiple containers.

<h2>Getting started</h2>
Docker provides a good and deep <a href="https://docs.docker.com/engine/docker-overview/">docs portal</a>, and is open source with a support coming from the community. 

Oh, I recommend to see their video on the <a href="https://www.youtube.com/user/dockerrun">Youtube</a> channel, it puts ligth on some common questions.

I have particularly appreciated this:
<iframe width="560" height="315" src="https://www.youtube.com/embed/IK3l9UhwOGU" frameborder="0" allowfullscreen></iframe>