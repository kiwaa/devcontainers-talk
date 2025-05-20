---
marp: true
---

# Build It like You Ship It

## Dev Containers

### Eugene Isakov

---

# Introduction

<!--
Short introduction, something like this:

Hi everyone, I'm Eugene Isakov, a developer within Quant Technology team. Today I want to share with you how you can leverage Docker as your dev environment. Being conscious of time, I would skip a lot of details, but feel free to ask questions at the end, message me in the Teams or find me on the 4th floor near meeting room D

Without further a do, let's begin
-->

---

# Docker is Great, But Your Dev Loop Can Be Better

<!-- In one sentence:
- We could use Docker containers for development, but they are lacking "dev experience" support
 -->

![bg right 40% complex stack](https://d2908q01vomqb2.cloudfront.net/ca3512f4dfa95a03169c5a670a4c91a19b3077b4/2020/03/11/prasanna_f2_2020_03_11_150.png)

### complex ML stack
- README.md
- language specific (`conda`)
- Dockerfile

<!--
As an example I would be using a ML application. 

- Classic approach would be to describe step by step how to configure the system, what needs to be installed, and how to deploy an application. Thanks to Docker technology, we describe it in one place, build it once and then ship it everywhere.

Sounds good, right? But we still use that classic approach for our local development. But documentation tends to get outdated, we could have conflicting dependencies or, your laptop could just die. That's actually happened to me 2 times in the past year.

You could argue, there are existing solutions like conda environments and we could run everything inside Docker, but both approaches have they own limitations.

What if I tell you, there is a better way, when you could have full development experience, including code completion, formatting, linting at your finger tip?

Let me introduce to you - Dev Containers. Tool that leverages same docker technology that we're using for production to provide familiar dev experience. Tool that allows you to fix bugs in production, but locally

-->

---

# What Are Dev Containers?

<!-- in one sentence 
- It is a docker-container with added layer to provide IDE integration
-->

- https://containers.dev/ - an open specification

### Key components
- an IDE that supports Dev Containers
- **Dockerfile** (or image)
- .devcontainer/devcontainer.json 

<!--

So what are they? 

First of all, dev containers are Docker-based development environments **defined by configuration files**.

Second, it's an [open specification](https://containers.dev/) for enriching containers with development specific content and settings. Tools like VS code can launch this setup automatically for the developer

There are 3 key components to it all:
- you need an IDE or code editor that supports Dev Containers. In my presentation I would be using vscode with dev containers extension
- **Dockerfile** (or image). After all, dev containers are Docker containers
- .devcontainer/devcontainer.json: this is a key, a configuration file that defines what should be applied on top of Dockerfile to create that "development environment". 

-->

---
# What Are Dev Containers?
## How it works?

<!-- in one sentence 
- essentially it's a type of remote development, where your IDE provides local UI 
-->

![VS Code setup](https://user-images.githubusercontent.com/10041279/93239062-e1b9a480-f747-11ea-94fb-3d50b14fd9b1.png)

<!--

How does it work?

It's essentially a remote development. You could replicate it all yourself, but it's just nice how its already pre-packaged for you.

When you open your dev container first time, VS Code Server got installed inside container that enables remote development experience, and your local VS Code connects to it. Your code is bind mounted inside container.


[META COMMENT]
some comparison / evolution of devcontainers vs CloudIDE , remove ssh (vs code)
jupyter notebook / lab: it was already "dev container"

-->

---

# Why Use Dev Containers? 
## Leveling Up Your Docker Workflow for Development

<!-- in one sentence
- We could get same benefits as in production
-->

- Environment Parity
- Consistency
- Reproducibility
- Project-specific, Isolated environments.
- Ephemeral containers
  
<!--

If you're not impressed by now, let me try a bit harder. Here is what you can get almost at no cost:

- Environment Parity. Dev containers achieves it by shifting containerization to left. You take production image, add something to get CI image, then you add more to get development image. Now if you have production issue or even CI issue, you could easily fix them on your machine
- Consistency and Reproducibility. Your environment is version-controlled, you could easilty switch between machines or even move to cloud. Everyone on the team has the same OS, system libraries, runtimes and even tooling. 
- Project-specific, Isolated environments.
  - each project get its pristine, tailored environment; you could pre-configure tools and extensions. Linters and debuggers are ready-to-go. - It also means you could have seamless context switching as each project has it's own perfect setup
  - you would have clean host machine. no need to install multiple versions of node.js, python, java, etc
- Ephemeral containers. Install anything you need right now to get job done and then start fresh.
  - you can easily test different versions; just update dockerfile or dev container and rebuild it

-->
---

# Getting Started 
## Demo

- Github: miscrosoft/vscode-remote-try-*

<!--
vscode-remote-try-rust

1. Clone repo →
2. VS Code detects devcontainer.json →
3, Reopen in container →


inside devcontainer:
- terminal
  - `uname -a` / `cat /proc/version`
  - file system (/workspace and /vscode)
  - `rustc -h` and `rustfmt -h`
- src/main
  - breakpoint
  - debugging
  - watch
- devcontainer.json
  - mention rich customizations
  - mention environment variables
  - extensions

codespaces
- github
  - press '.'
- vscode slim
  - 'open in new codespaces'
  - 'open in vscode'

-->

---

# Final notes

- https://containers.dev/
- https://code.visualstudio.com/docs/devcontainers/containers
  - vscode: `F1` -> "Add Dev Container Configuration Files..."

<!--

Imagine, that tomorrow you come to work and all repositories have a dev container config. You could launch a perfect setup under a few minutes, even if you never worked with repository. You could try technologies or setups that other teams are using and feel like you're a member of that team. Nothing blocks you from being creative and productive, at least from environment perspective.

I encourage you to try dev containers. Either just check out one of microsoft examples or follow easy step-by-step setup inside vscode.

Thank you

-->
---

# Q & A