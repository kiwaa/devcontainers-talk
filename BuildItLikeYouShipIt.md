## Docker Is Great, But Your Dev Loop Can Be Better

Long time ago, people could spend days preparing production environment to fresh app deployment. Everything changed with Docker and containerization technology. Industry 

Some time ago, it was a common challenge: develop an app locally and then be able to reliably ship it to production. Nowadays, thanks to Docker and genius idea to ship whole machine, we could spend more time delivering value and spend less time managing dependencies.

But in same time, there is a disconnect: we have reliable deployments, but our local setup is plagued by the same issues we had in production in the past. Any day we could receive a security update, install new version of library or accidentally remove environment variable that we set 2 years ago.

Or, your laptop could just die. That's actually happened to me 2 times in the past year.

But even if you don't have complicated setup and you already using Dockerfile or docker-compose to spin up all dependencies for your projects, you still may need to open console windows, use separate conda env or be forced somehow tweak configs to make it work.

What if it's a better way, when all things could be seamlessly integrated in your IDE?

Let me introduce to you - Dev Containers. A way to fix bugs in production, but locally

##  What Are Dev Containers?

So what are they? 

First of all, dev containers is an open specification that could be implemented by anyone. It's a way to introduce tooling, configuration and other bits that are necessary to create traditional development experience.

Second, it's essentially a remote development. You could replicate it all yourself, but it's just nice how its already pre-packaged for you.

There are 3 key components to it all:
- **Dockerfile** (or image). After all, dev container is just a Docker container
- .devcontainer/devcontainer.json: this is a key, a configuration file that defines what should be applied on top of Dockerfile to create "development environment". In specification, they some times call it "metadata"
- finally, you need an IDE that support Dev Containers

I'll be talking about VS Code, as it's what I'm using and I know it's working. Another big player is Jetbrains, but I didn't use it.

How does it work? As I mentioned, it's a form of remote development, when VS Code Server got installed inside container that enables remote development experience, and your local VS Code connects to it. Your code is bind mounted inside container.

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

## 