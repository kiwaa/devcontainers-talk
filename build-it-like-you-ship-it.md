## Docker Is Great, But Your Dev Loop Can Be Better

Some time ago, it was a common challenge: develop an app locally and then be able to reliably ship it to production. Nowadays, as containerizing production workloads becomes commonplace, we could spend more time delivering value and spend less time managing dependencies.

But in the same time, there is a disconnect: we have reliable deployments, but our local setup is plagued by the same issues we had in production in the past. Any day we could receive a security update, install new version of library or accidentally remove environment variable that we set 2 years ago.

Or, your laptop could just die. That's actually happened to me 2 times in the past year.

![complex stack](https://d2908q01vomqb2.cloudfront.net/ca3512f4dfa95a03169c5a670a4c91a19b3077b4/2020/03/11/prasanna_f2_2020_03_11_150.png)

Picture this: you have a complex development setup. In this example, it's a ML stack with heavy dependencies on native libraries and hardware. You want to spend time in your code, but you environment could become completely broken because you want to test new version of one of this libraries. Existing solutions like conda environments could solve this only partially.

Another issue arise, when you want to share results with your colleague. [..]

What if it's a better way, when all things could be seamlessly integrated in your IDE?

Let me introduce to you - Dev Containers. A way to fix bugs in production, but locally

n specific terms, dev containers are Docker containers (running locally or remotely) that encapsulate everything necessary for the software development of a given project, including integrated development environments (IDEs), specific software, tools, libraries, and preconfigured services. 

<!-- jupyter notebook / lab: it was already "dev container"-->

##  What Are Dev Containers?

So what are they? 

First of all, dev containers are Docker-based development environments **defined by configuration files**. Tools like VS code can launch this setup automatically for the developer

Second, it's an [open specification](https://containers.dev/) for enriching containers with development specific content and settings. 

There are 3 key components to it all:
- **Dockerfile** (or image). After all, dev container is just a Docker container
- .devcontainer/devcontainer.json: this is a key, a configuration file that defines what should be applied on top of Dockerfile to create "development environment". In specification, they some times call it "metadata"
- finally, you need an IDE that support Dev Containers

I'll be talking about VS Code, as it's what I'm using and I know it's working. Another big player is Jetbrains, but I didn't use it.

How does it work? 


It's essentially a remote development. You could replicate it all yourself, but it's just nice how its already pre-packaged for you.

When you launch your devcontainer first time, VS Code Server got installed inside container that enables remote development experience, and your local VS Code connects to it. Your code is bind mounted inside container. After that you could build, run and debug your application inside the container. What is also great, you could open multiple terminal windows inside that container, install additional ad-hoc tools, etc

As part of devcontainer configuration file, you could customize extensions and settings, to get that tailored environment I mentioned before.

<!-- some comparison / evolution of devcontainers vs CloudIDE , remove ssh (vs code)
-->

## Why Use Dev Containers? Levelling Up Docker Workflow for Development

If you're not impressed by now, you either don't have a problem I described in the beginning or you don't think it's such a big problem. Here is what you can get out of it:

- Environment Parity. Docker idea is to take development machine and ship it to production, dev containers shift everything left. You take production image, add something to get CI image, then you add more to get development image. Now if you have production issue or even CI issue, you could easily fix them on your machine
- Consistency. everyone on the team has the same OS, system libraries, runtimes and even tooling. If you rely on conda environment, it doesn't control all native dependencies you could have
- Reproducibility. environment is version-controlled. New joiner can get up and running in minutes. You could easily switch machines or even move to cloud. More about it later. It's also a form of formalized knowledge that could be shared, assessed and evolving over time
- Project-specific, Isolated environments.
  - each project get its pristine, tailored environment; you could pre-configure tools and extensions. Linters and debuggers are ready-to-go. - It also means you could have seamless context switching as each project has it's own perfect setup
  - you would have clean host machine. no need to install multiple versions of node.js, python, java, etc
  - you can easily test different versions; just update dockerfile or dev container and rebuild it
- Ephemeral containers. Install anything you need right now to get job done and then start fresh.

## Why Not Use Dev Containers?

It's great solution, but as everything has limitations and trade-offs.

Running docker containers naturally means that you have resource overhead. You still could leverage dev containers, we would talk about it in a few minutes

If your project is simple or lightweight, you also don't need that overhead.

lastly, if you're doing mobile development or have dependencies that do not work correctly in containers.
