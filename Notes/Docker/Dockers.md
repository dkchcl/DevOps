## Docker:

**What is Docker?**

Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. Docker is a platform designed to help developers build, share, and run container applications. 

1. Docker is an open-source Centralised Plateform, designed to Create, Deploy and run applications.
2. Docker uses Container on the host OS to run applications, It allows applications to use the same Linux Kernel as a system on the host Computer, rather than creating a whole Virtual OS.
3. We can install Docker on any OS but Docker Engine runs natively on Linux Distribution.
4. Docker written in 'go' Language.
5. Docker is a tool that performs OS level Vertualization, also known as Containerization.
6. Before Docker many users faces the problem that a particular code is running in the developer's system but not in the user's system.
7. Docker was first release in March 2013, it is developed by Solomon Hykes and Sebastien Pahl.
8. Docker is a set of Platform as a Service (PaaS) that uses OS Level Virtualization whereas VMware uses Hardware level Virtualization.
   
**Why Docker is popular?**

Docker gained its popularity due to its impact on the software development and deployment. The following are the some of the main reasons for docker becoming popular:

**Portability:** Docker facilitates the developers in packaging their applications with all dependencies into a single lightweight containers. It facilities in ensuring the consistent performance across the different computing environments.

**Reproducibility:** Through encapsulating the applications with their dependencies within a container it ensures in software setups remaining consistent across the development, testing and production environments.

**Efficiency:** Docker through its container based architecture it optimizes the resource utilization. It allows the developers to run the multiple isolated applications on a single host system.

**Scalability:** Docker’s scalability features facilitated the developers in making easier of their applications handling at time of workloads increment.

#### Container:

**what is Container?**

A container is simply an isolated process with all of the files it needs to run. If you run multiple containers, they all share the same kernel.
A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings. A Docker container is a standardized, encapsulated environment that runs applications. A container is managed using the Docker API or CLI.

#### Docker Desktop:

Docker Desktop is a one-click-install application for your Mac, Linux, or Windows environment that lets you build, share, and run containerized applications and microservices.

It provides a straightforward GUI (Graphical User Interface) that lets you manage your containers, applications, and images directly from your machine.

Docker Desktop reduces the time spent on complex setups so you can focus on writing code. It takes care of port mappings, file system concerns, and other default settings, and is regularly updated with bug fixes and security updates.

**What's included in Docker Desktop?**
Docker Engine
Docker CLI client
Docker Scout (additional subscription may apply)
Docker Build
Docker Extensions
Docker Compose
Docker Content Trust
Kubernetes
Credential Helper

**What are the key features of Docker Desktop?**
Ability to containerize and share any application on any cloud platform, in multiple languages and frameworks.
Quick installation and setup of a complete Docker development environment.
Includes the latest version of Kubernetes.
On Windows, the ability to toggle between Linux and Windows containers to build applications.
Fast and reliable performance with native Windows Hyper-V virtualization.
Ability to work natively on Linux through WSL 2 on Windows machines.
Volume mounting for code and data, including file change notifications and easy access to running containers on the localhost network.

**Docker Desktop Installation**
Download Docker Setup for windows "Desktop for Windows - x86_64" and install on your windows/ or download linux setup for linux pc.

after installation check docker version--

```powershell
docker --version
```

**Download Imager from Docker Hub:**

```powershell
docker pull nginx
```

### Create a Container:

```powershell
docker run --help
```

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```powershell
docker run --detach --name dineshold_pc nginx
```

#### Show containers Details:

Show all containers (default shows just running)
```powershell
docker ps -a
```
```powershell
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
a15a58e7dbd0   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   80/tcp    dineshnew_pc
499a3a630743   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    dineshold_pc
```
Show the latest created container (includes all
                        states)
```powershell
PS D:\mydata\terraform_code> docker ps -l
```
```powershell
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
a15a58e7dbd0   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    dineshnew_pc
```
Only display container IDs
```powershell
PS D:\mydata\terraform_code> docker ps -q
```
```powershell
a15a58e7dbd0
499a3a630743
```
Display total file sizes
```powershell
PS D:\mydata\terraform_code> docker ps -s
```
```powershell
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES          SIZE
a15a58e7dbd0   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    dineshnew_pc   81.9kB (virtual 207MB)
499a3a630743   nginx     "/docker-entrypoint.…"   5 minutes ago   Up 5 minutes   80/tcp    dineshold_pc   81.9kB (virtual 207MB)
```
Don't truncate output---
```powershell
docker ps --no-trunc
```
```powershell
CONTAINER ID                                                       IMAGE     COMMAND                                          CREATED         STATUS         PORTS     NAMES
a15a58e7dbd04e303b1c854261c5d88544a0241bad4bac30e0d89035af33cc1c   nginx     "/docker-entrypoint.sh nginx -g 'daemon off;'"   7 minutes ago   Up 7 minutes   80/tcp    dineshnew_pc
499a3a630743d7db57b8cd9a4a5471e87c827506c615cfe49dbe5d4853523ade   nginx     "/docker-entrypoint.sh nginx -g 'daemon off;'"   9 minutes ago   Up 9 minutes   80/tcp    dineshold_pc
```

### Syntax to go in Container using Linux Command:

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

**Example:**
```powershell
docker exec -i -t dineshold_pc bash
docker exec -i -t dineshold_pc ls
docker exec -i -t dineshold_pc sh
```



### Remove unused data:
```powershell
docker system prune --help
```
Usage:  docker system prune [OPTIONS]

Remove unused data
```powershell
Options:
  -a, --all             Remove all unused images not just dangling ones
      --filter filter   Provide filter values (e.g. "label=<key>=<value>")
  -f, --force           Do not prompt for confirmation
      --volumes         Prune anonymous volume
```

**Example:**
```powershell
docker system prune -a -f 
```



