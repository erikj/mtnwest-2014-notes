# Trip Report: MountainWest DevOps Conference, March 19, 2014, Salt Lake City, Utah


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

- **autoconf**: ./configure
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

