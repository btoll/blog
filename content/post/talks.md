+++
date = "2018-06-07T08:09:26-07:00"
title = "Talks"
author = "Jessica Frazelle"
description = "Various Talks I have given on containers, container security, Docker, Kubernetes, and Open Source."
featured = true
+++

I figured it would be nice to have one canonical place for talks I have given.
So here it is...

## 2019

### [CERN - Why Open Source Firmware is Important](https://indico.cern.ch/event/819789/)

This talk will dive into some of the problems of running servers at scale, including data from surveys about physical infrastructure and firmware concerns. In this talk, we'll understand how open source firmware will solve some of these common problems. Why is open source firmware important for security and root of trust? We'll discuss that as well, and cover the state of open source firmware today.

### [QCon London - Panel: Secure Isolation of Applications](https://www.infoq.com/presentations/secure-isolation-applications/)

**Co-Speakers: Justin Cormack, Per Buer, Allison Randal, Kenton Varda**

Applications have been isolated by lots of different means: processes, virtual machines, containers, and new methods are appearing such as SGX and in-process isolates. What is secure? Have Spectre and Meltdown changed the landscape? What should be used?

### [QCon London - A Journey into Intel’s SGX](https://www.infoq.com/presentations/intel-sgx/)

This talk takes a deep dive into Intel's SGX technology. It covers an overview of computer architecture as background and walks the audience through one version of the hardware and its flaws, as well as what changed in the next version.

## 2018

### [re:Invent - Container Power Hour](https://www.youtube.com/watch?v=HCCkVz25UU4)

**Co-Speakers: [Clare Liguori](https://twitter.com/clare_liguori) and [Abby Fuller](https://twitter.com/abbyfuller)**

This talk goes over using containers on AWS.

### [ChaosConf - Breaking Containers](https://www.youtube.com/watch?v=1hhVS4pdrrk&list=PLLIx5ktghjqKtZdfDDyuJrlhC-ICfhVAN&index=11)

Chaos engineering and stories of bugs about containers.

### [LinuxConfAu - Containers aka crazy user space fun](https://www.youtube.com/watch?v=7mzbIOtcIaQ)

Like the movie Plan 9 from outer space, this talk covers containers from 
user space. What are they? Where did they come from?
How much koolaid is involved in adopting them into your life... watch for the 
jokes, learn from the interesting technical details.

## 2017

### [Google Cloud Next - Build user trust: running containers securely](https://www.youtube.com/watch?v=Cd4JU7qzYbE)

**Co-Speaker: Alex Mohr**

This talk covers all the ways you can secure your Kubernetes cluster using a
Certificate Authority, Authentication, Secrets and more. We  also describe and
demonstrate the ways you can use Seccomp, AppArmor, SELinux and cgroups to make
your application containers as secure as possible - so you can build organizational
and customer trust.

### [CoreOS Fest - Container Linux on the Desktop!](https://www.youtube.com/watch?v=gES4-X6y278)

This talk covers how to build a secure desktop OS with only containers and
CoreOS Container Linux. It also describes the benefits gained from using
Container Linux as a base OS and how to go about running it on the desktop.

### [Kubecon - Dance Madly on the Lip of a Volcano](https://www.youtube.com/watch?v=sNjylW8FV9A)

**Co-Speaker: [Brandon Philips](https://twitter.com/BrandonPhilips)**

This talk covers how we designed an awesome security release process for
Kubernetes and all it’s sub-projects.

Open source projects strive to be transparent in everything they do, but when
it comes to fixing security patches they need to find the right balance of
“open” and “responsible.” This means vulnerabilities should be reported in
a safe way as well as patches tested and reviewed with a limited audience. The
companies that rely on Kubernetes should have time to patch their systems
before a public announcement.

Various sets of infrastructure and collaboration are needed to make this
a reality. The design we used could also be applied to other projects and even
internally in your company.

## 2016

### [Container Summit - Building Containers in Pure Bash and C](https://containersummit.io/events/nyc-2016/videos/building-containers-in-pure-bash-and-c)

This talk demonstrates how to build containers from the Primitives in Linux
without using a container runtime. Learn about the objects that make up
containers themselves.

### [Arrested DevOps - Exciting Topics like Containers & Security](https://www.youtube.com/watch?v=qPs5U5hdciM)

[Ben Hughes](https://twitter.com/benjammingh) and I chat with
[Bridget Kromhout](https://twitter.com/bridgetkromhout) about everyone's
favorite topic, security.

### [Github Universe - Blurry lines between individual contributor & corporate backers](https://www.youtube.com/watch?v=4Iem6JK6PtY)

When working on open source projects, your contributions and opinions on the
project and its motives are usually very personal. This talk
covers intricacies of "choosing your battles" and how personal passion for
a project might conflict with corporate motives.

### [Container Camp - Application Sandboxes vs. Containers](https://www.youtube.com/watch?v=mfnhSX6SJVA)

This talk covers the differences between application sandboxes and containers.
The most well known sandbox is Chrome, for providing "hard guarantees about what
ultimately a piece of code can or cannot do no matter what its inputs are".

At its core, the Linux Chrome sandbox uses namespaces along with seccomp and
other native features to provide these guarantees. Containers are composed of
the same primitives. What is needed for containers to provide this promise?
Can it be done by default? What steps are already being made to get towards
containers that actually "contain"? What challenges will be faced?

## 2015

### [Dockercon EU - The Latest in Docker Engine](https://www.youtube.com/watch?v=I7i4SY-iRkA)

**Co-Speaker: [Arnaud Porterie](https://twitter.com/icecrime)**

Learn about the latest capabilities in Docker Engine and how to use them in
your application. This session also covers best practices for using Engine,
troubleshooting tips, and cool lesser known features.

This video has the first ever demo of Seccomp in Docker as well as a fun story
about trying to save a docker image to a floppy disk.

### [DockerCon - Container Hacks and Fun Images](https://www.youtube.com/watch?v=cYsVvV1aVss)

This talk is a 100% live demo of running desktop applications in containers.
Everything from Spotify to Skype. Explore some of the more interesting things
you can containerize on Linux. View first hand different workflows for how to
run/build different apps in containers. This talk covers desktop apps as well
as some other apps you would have never thought could run in a container.

### [Container Camp - Willy Wonka of Containers](https://www.youtube.com/watch?v=GsLZz8cZCzc)

This talk has live demos of desktop applications in containers including Steam.

### [HashiConf - Dockerizing all the Things](https://www.youtube.com/watch?v=PeE8hcQtFq4)

This talk goes over the way the Docker project uses containers for their
testing infrastructure as well as internal infrastructure. Find out about real
pain points solved by running things in containers as well as some different
hurdles uncovered along the way.

### [DotGo - The Docker Trail](https://www.youtube.com/watch?v=j55aWjgzfV8)

This talk recounts stories from the trenches of developing Docker, explaining 3
odd things her team stumbled upon in their Go code and how they fixed them. One
of which is very odd and gets into the depths of `dlopen`-ing yourself.

### [Google Cloud Platform Podcast - Containers](https://www.youtube.com/watch?v=zu8NSrNFZ4M)

[Francesc Campoy](https://twitter.com/francesc) and I talk all about
Dockercon EU and containers.
