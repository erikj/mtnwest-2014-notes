# Trip Report: MountainWest DevOps Conference, March 19, 2014, Salt Lake City, Utah

The third day of MountainWest Hackweek was the MountainWest DevOps Conference, which covered contemporary and bleeding-edge techniques and best practices of [DevOps](http://en.wikipedia.org/wiki/DevOps).

All of the presentations delivered were high quality and informative. This report covers what I consider to be the highlights. If interested in complete coverage of this conference, I direct the reader to [my conference notes](https://github.com/erikj/mtnwest-2014-notes/blob/master/TODAY-20140319.md)

## Modern DevOps: Understanding the Terrain

Mitchell Hashimoto, creator and maintainer [**Vagrant**](http://vagrantup.com) started the DevOps conference by presenting on the current landscape and lifecycle of DevOps, highlighting where the tools of the DevOps company that he founded, Hashicorp, fit in. Those tools are:

- [**Vagrant**](http://vagrantup.com)
- [**Packer**](http://www.packer.io/)
- [**Serf**](http://www.serfdom.io/)

Mitchell described the modern lifecycle of an application (excluding retirement / EOL) as:

- **development**, when we want application development environments to be:
  - readily available-- shouldn't take hours or days for new developer or new application to be set up for development
  - make changes, see changes
  - consistent
    - want to avoid: "well, it works on my machine"
  - collaboration and sharing: working w/ others, sharing work w/ others
- **deployment**
  - run on test, staging or production
  - start / configure servers
  - deliver / run application
- **maintenance**: keep everything running and changing
  - monitoring
    - anticipate and react to problems before they become big problems
  - updating
    - OS
    - libraries
    - application
  - orchestrating resources and services

The goal of DevOps is to make this application lifecycle more efficient and optimized for efficiency. This is accomplished via tools, which:

- reduce human error
- increase repeatability
- codify of knowledge
- are faster

### Tour Of Tools

#### Development

**Vagrant** allows developers to clone a project repository or install a ready-to-go operating-system image packaged as a Vagrant Box, run `$ vagrant up`, and quickly have a readily available, consistent, development environment.

**Vagrant** development environments are also shareable via [`vagrant share`](http://docs.vagrantup.com/v2/share/index.html) and [`vagrant connect`](http://docs.vagrantup.com/v2/share/connect.html), which were [added w/ the recently released Vagrant 1.5](http://www.vagrantup.com/blog/feature-preview-vagrant-1-5-share.html):

> The `share` command is used to share a running Vagrant environment, and the `connect` command compliments it by accessing any shared environment. 

#### Deployment

Deployment tools are more varied and slightly more complicated:

- **autoconf**: `./configure`
- configuration management tools:
  - chef
  - puppet
  - salt
  - ansible
  - etc.
- [Packer](http://packer.io)
  - optimizes slow parts of server set up by creating images
    - DevOps has historically been against images
      - hard to apply changes to running image
        - led to move to modern CM
      - benefits
        - super-fast infrastructure deployment
        - stability, testability
    - able to build images for everything using every CM tool
- Docker

#### Maintenance

The common goal of maintence tools is to change w/ resiliency to failure.

- one way to do this: **Serf**:
  - > Serf is a decentralized solution for service discovery and orchestration that is lightweight, highly available, and fault tolerant.

  - manages membership, lets you know when membership changes
  - [gossip](http://www.serfdom.io/docs/internals/gossip.html)-based membership
    - every node checks a random node
    - broadcasts checked node's status to cluster
  - custom events: used to trigger deploys, propagate configuration, etc
  - result: resilient to failure, near instant notification

## [What Your Mother Never Told You About Automating Security](https://github.com/jro/automated_security/blob/master/presentation/one/01_slide.md) ([`pdf`](https://github.com/jro/automated_security/blob/master/presentation.pdf?raw=true))

Jason Rohwedder, of [Risk I/O](https://www.risk.io/), delivered a presentation on automating security. Automation is needed because:

> Security is hard. Be methodical. It takes time.

This presentation covered his experience w/ and knowledge of tools and techniques that addressed the following areas:

- network security
- network access
- host firewalls
- auto firewalls (`fail2ban`)
- Denial-of-Service / Distributed-Denial-of-Service protection
- Bastion / gateway hosts
- SSH (*"use keys, not passwords."*)
- `sudo`
- automatic software updates
  - pin / free critical or unreliable packages
- OS hardening, *e.g.* SELinux and `sysctl`
- intrusion-detection systems
- encryption of resting data
  > in the cloud, we don't know where our hard drives are going to go after they leave our EC2 instances
- encryption of backups
- centralized logging
- static analysis
- host-vulnerability scanning
- web-application vulnerability scanning

Listing all of the tools covered herein would be excessively verbose and redundant. I direct the reader to [the slides for this presentation](https://github.com/jro/automated_security/blob/master/presentation/one/01_slide.md) ([`pdf`](https://github.com/jro/automated_security/blob/master/presentation.pdf?raw=true)) for the descriptions of the techniques and links to the tools covered for the topics for which the reader might be interested.

## The Immutable Pipeline

Chris Gaffney, of Collective Idea, presented on using [Packer](http://www.packer.io/) to create immutable (compiled) machine images for deployment to staging and operations environments.

Machine images are initialized using Packer, then provisioned in Chef (solo). The goal is to create an image upon which Chef never needs to be run again. Compiled images are then tested as black boxes using RSpec, which makes HTTP requests to the images' API via the [Faraday](https://github.com/lostisland/faraday) Ruby gem. Images are deployed to staging continuously, operations when ready and then destroyed when they are no longer needed or superseded by updated images.

## Introduction to Docker

James Turnbull provided an introduction to [Docker](https://www.docker.io/), which provides a convenient interface to Linux Containers, which have been around since Linux 2.6, but require extensive knowledge of the kernel and cgroups to be accessed.

Addressing the excitement and utility, James said:

> Containerization is the new virtualization

Docker adopts its concept from Solaris:

- easy and lightweight way to model reality
- devs care about their app, ops cares about containers
- golden images w/o the overhead

Docker containers offer several advantages over deployments that require VMs or Cloud:

- speed of deployment
  - containers are a fraction of the size of a virtual machine, which contains an entire OS, so they can be up/downloaded that much more quickly
- portability
  - containers can run on any supported version of Linux, don't require any virtualization software, *ie.* VMWare, VirtualBox, EC2, Hypervisor, etc. aren't required
- size aka cached layering
  - containers can be built on base-container images and deltas
- density & performance
  - run many containers on a single server / VM instance w/ no penalty for emulation, but still maintain the isolation of having separate services on separate VM or Cloud instances
- cost-- VMWare is expensive @ scale

Docker container images can be sourced from [public](https://index.docker.io/) or private registries. Container images are composed of layers and their deltas.

## ["DevOps" in a Post-DevOps World](http://www.slideshare.net/jpreed/mtnwest-devops2014)

Paul Reed, historically a build & release engineer, and a DevOps consultant for the last few years, and runs a podcast, [The Ship Show](http://theshipshow.com/), addressed the current hype surrounding DevOps and asked:

> Has [jumped the shark](http://en.wikipedia.org/wiki/Jumping_the_shark)?

Paul used the [Cynefin framework](http://en.wikipedia.org/wiki/Cynefin) to see how DevOps' classical set of values maps to practices and a new set of values.

DevOps' classical set of values are described by the *CAMS* acronym:

- Culture
- Automation
- Metrics
- Sharing

According to [wikipedia](http://en.wikipedia.org/wiki/Cynefin#Description_of_the_framework):

> The Cynefin framework has five domains. The first four domains are:

> 1. Simple, in which the relationship between cause and effect is obvious to all, the approach is to Sense - Categorise - Respond and we can apply best practice.

> 2. Complicated, in which the relationship between cause and effect requires analysis or some other form of investigation and/or the application of expert knowledge, the approach is to Sense - Analyze - Respond and we can apply good practice.

> 3. Complex, in which the relationship between cause and effect can only be perceived in retrospect, but not in advance, the approach is to Probe - Sense - Respond and we can sense emergent practice.

> 4. Chaotic, in which there is no relationship between cause and effect at systems level, the approach is to Act - Sense - Respond and we can discover novel practice.

> The fifth domain is Disorder, which is the state of not knowing what type of causality exists, in which state people will revert to their own comfort zone in making a decision. In full use, the Cynefin framework has sub-domains, and the boundary between simple and chaotic is seen as a catastrophic one: complacency leads to failure.

Paul uses Cynewin to show how *CAMS* maps to his new set of values, described by the *VIDS* acronym:

- Value realignment
- Individuality
- Don't be an asshole (*cf.* [The No Asshole Rule: Building a Civilized Workplace and Surviving One That Isn't](http://en.wikipedia.org/wiki/The_No_Asshole_Rule) by Stanford Professor of Management Science, Robert I. Sutton)
- Self awareness / Systems thinking
  - *cf.* [Empathy is a core engineering value](http://boingboing.net/2013/12/01/empathy-is-a-core-engineering.html)

Paul concludes that DevOps has become an established set of best practices, like Extreme Programming (XP), Agile / Scrum and LeanIT.
