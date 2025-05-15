---
marp: true
---

# Build It like You Ship It

## Dev Containers

**Eugene Isakov**

---

# Introduction

<!--
Short introduction, something like this:

Hi everyone, I'm Eugene Isakov, a developer within Quant Technology team. Today I want to share with you how you can leverage Docker as your dev environment. Being conscious of time, I would skip a lot of details, but feel free to ask questions at the end, message me in the Teams or find me in the corner of 4th floor near meeting room D
-->

---

# Docker is Great, But Your Dev Loop Can Be Better

![bg right 40% complex stack](https://d2908q01vomqb2.cloudfront.net/ca3512f4dfa95a03169c5a670a4c91a19b3077b4/2020/03/11/prasanna_f2_2020_03_11_150.png)

### complex ML stack
- conda solves it partially

<!--
Some time ago, it was a common challenge: develop an app locally and then be able to reliably ship it to production. Nowadays, thanks to Docker and genius idea to ship whole machine, we could spend more time delivering value and spend less time managing dependencies.

But in same time, there is a disconnect: we have reliable deployments, but our local setup is plagued by the same issues we had in production in the past. Any day we could receive a security update, install new version of library or accidentally remove environment variable that we set 2 years ago.

Or, your laptop could just die. That's actually happened to me 2 times in the past year.

Let's have a look at complex development setup. In this example, it's a Machine Learning stack that depends on GPU. You want to spend time in your code, but forced to keep an eye on all this components. Existing solutions like conda environments could solve this partially.

What if it's a better way, when all things could be seamlessly integrated in your IDE?

Let me introduce to you - Dev Containers. A way to fix bugs in production, but locally
-->

---

# What Are Dev Containers?


- Docker-based development environments **defined by configuration files**
- an [open specification](https://containers.dev/)


There are 3 key components to it all:
- **Dockerfile** (or image)
- .devcontainer/devcontainer.json: 
- an IDE that support Dev Containers

<!--

So what are they? 

First of all, dev containers are Docker-based development environments **defined by configuration files**. Tools like VS code can launch this setup automatically for the developer

Second, it's an [open specification](https://containers.dev/) for enriching containers with development specific content and settings. 

It's essentially a remote development. You could replicate it all yourself, but it's just nice how its already pre-packaged for you.

There are 3 key components to it all:
- **Dockerfile** (or image). After all, dev container is just a Docker container
- .devcontainer/devcontainer.json: this is a key, a configuration file that defines what should be applied on top of Dockerfile to create "development environment". In specification, they some times call it "metadata"
- finally, you need an IDE that support Dev Containers

I'll be talking about VS Code, as it's what I'm using and I know it's working. Another big player is Jetbrains, but I didn't use it.

How does it work? As I mentioned, it's a form of remote development, when VS Code Server got installed inside container that enables remote development experience, and your local VS Code connects to it. Your code is bind mounted inside container.

some comparison / evolution of devcontainers vs CloudIDE , remove ssh (vs code)
jupyter notebook / lab: it was already "dev container"
-->

---
# What Are Dev Containers?
## How it works?

![VS Code setup](https://user-images.githubusercontent.com/10041279/93239062-e1b9a480-f747-11ea-94fb-3d50b14fd9b1.png)


---

# Why Use Dev Containers? 
## Leveling Up Your Docker Workflow for Development

- Environment Parity
- Consistency
- Reproducibility
- Project-specific, Isolated environments.
- Ephemeral containers
  
---

# Why Not Use Dev Containers

- Mobile and Windows-native development
- Single developer
- Performance

<!-- 
- Mobile and Windows-native development: Emulators needed for that type of development don’t work as well as they do on a host machine.
- Single developer: Many of the benefits of Dev Containers are most evident when there are multiple contributors to the same project.
- Performance: There might be some performance hiccups, but there are solutions.

-->

---

# Getting Started 
## Demo

---

# Understanding devcontainer.json

## Quick Overview