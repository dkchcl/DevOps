## Docker:


1. Docker is an open-source Centralised Plateform, designed to Create, Deploy and run applications.
2. Docker uses Container on the host OS to run applications, It allows applications to use the same Linux Kernel as a system on the host Computer, rather than creating a whole Virtual OS.
3. We can install Docker on any OS but Docker Engine runs natively on Linux Distribution.
4. Docker written in 'go' Language.
5. Docker is a tool that performs OS level Vertualization, also known as Containerization.
6. Before Docker many users faces the problem that a particular code is running in the developer's system but not in the user's system.
7. Docker was first release in March 2013, it is developed by Solomon Hykes and Sebastien Pahl.
8. Docker is a set of Platform as a Service (PAAS) that uses OS Level Virtualization whereas VMware uses Hardware level Virtualization.
   


```powershell
docker pull nginx
```
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



