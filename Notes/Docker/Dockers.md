## Docker:



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

### Uses to go in Container using Linux Command:

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

docker exec -i -t dineshold_pc bash








### Remove unused data:

docker system prune --help

Usage:  docker system prune [OPTIONS]

Remove unused data

Options:
  -a, --all             Remove all unused images not just dangling ones
      --filter filter   Provide filter values (e.g. "label=<key>=<value>")
  -f, --force           Do not prompt for confirmation
      --volumes         Prune anonymous volume






