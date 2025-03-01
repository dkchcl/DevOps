## Docker Commands:

docker --help

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

#### Common Commands:

**run**          # Create and run a new container from an image
```powershell
docker run --help
```
Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```powershell
docker run --detach --name dineshold_pc nginx
```
**exec**        # Execute a command in a running container
  
  ```
  docker exec --help
  ```
  Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

**Example:**
```powershell
docker exec -i -t dineshold_pc bash
docker exec -i -t dineshold_pc ls
docker exec -i -t dineshold_pc sh
```
**ps**          # List containers
```
docker ps --help
```
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
```
CONTAINER ID                                                       IMAGE     COMMAND                                          CREATED         STATUS         PORTS     NAMES
a15a58e7dbd04e303b1c854261c5d88544a0241bad4bac30e0d89035af33cc1c   nginx     "/docker-entrypoint.sh nginx -g 'daemon off;'"   7 minutes ago   Up 7 minutes   80/tcp    dineshnew_pc
499a3a630743d7db57b8cd9a4a5471e87c827506c615cfe49dbe5d4853523ade   nginx     "/docker-entrypoint.sh nginx -g 'daemon off;'"   9 minutes ago   Up 9 minutes   80/tcp    dineshold_pc
```
  **build**       Build an image from a Dockerfile
```
 docker build --help
```
  ```
  Usage:  docker buildx build [OPTIONS] PATH | URL | -
  ```
**pull**        Download an image from a registry
```
docker pull --help
```
```
Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
**push**        Upload an image to a registry
```
docker push --help
```
```
Usage:  docker push [OPTIONS] NAME[:TAG]
```

**images**      List images
```
docker images --help
```
```
Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]
```
```
Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Format output using a custom template:
                        'table':            Print output in table format
                        with column headers (default)
                        'table TEMPLATE':   Print output in table format
                        using the given Go template
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using the given
                        Go template.
                        Refer to https://docs.docker.com/go/formatting/
                        for more information about formatting output with
                        templates
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
      --tree            List multi-platform images as a tree (EXPERIMENTAL)
```
**login**       Authenticate to a registry
```
docker login --help
```
```
Usage:  docker login [OPTIONS] [SERVER]
```
```
Authenticate to a registry.
Defaults to Docker Hub if no server is specified.

Options:
  -p, --password string   Password
      --password-stdin    Take the password from stdin
  -u, --username string   Username
```

**logout**      Log out from a registry
```
docker logout --help
```
```
Usage:  docker logout [SERVER]
```
Log out from a registry.
If no server is specified, the default is defined by the daemon.  

**search**      Search Docker Hub for images
```
docker search --help
```
```
Usage:  docker search [OPTIONS] TERM
```
Search Docker Hub for images
```
Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results
      --no-trunc        Don't truncate output
```
**version**     Show the Docker version information
```
docker version --help
```
```
Usage:  docker version [OPTIONS]
```
Show the Docker version information
```
Options:
  -f, --format string   Format output using a custom template:
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using the given
                        Go template.
                        Refer to https://docs.docker.com/go/formatting/
                        for more information about formatting output with
                        templates
```
**info**        Display system-wide information
```
docker info --help
```
```
Usage:  docker info [OPTIONS]
```
Display system-wide information

Aliases:
  docker system info, docker info
```
Options:
  -f, --format string   Format output using a custom template:
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using the given
                        Go template.
                        Refer to https://docs.docker.com/go/formatting/
                        for more information about formatting output with
                        templates
```

#### Management Commands:

  ai*         Ask Gordon - Docker Agent

  builder     Manage builds

  buildx*     Docker Buildx
  
  
  checkpoint  Manage checkpoints
  
  compose*    Docker Compose
  
#### **container**   Manage containers
```
docker container --help
```
```
Usage:  docker container COMMAND
```
#### Manage containers

**Commands:**

**attach**  Attach local standard input, output, and error streams to a running container
```
docker container attach --help
```
```
Usage:  docker container attach [OPTIONS] CONTAINER
```
Attach local standard input, output, and error streams to a running container

Aliases:
  docker container attach, docker attach
```
Options:
      --detach-keys string   Override the key sequence for detaching a
                             container
      --no-stdin             Do not attach STDIN
      --sig-proxy            Proxy all received signals to the process
                             (default true)
```                             
**commit**      Create a new image from a container's changes
```
docker container commit --help
```
**cp**          Copy files/folders between a container and the local filesystem
```
docker container cp --help
```
**create**      Create a new container
```
docker container create --help
```  
**diff**        Inspect changes to files or directories on a container's filesystem
```
docker container diff --help
```  
**exec**        Execute a command in a running container
```
docker container exec --help
```  
**export**      Export a container's filesystem as a tar archive
```
docker container export --help
```

  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Create and run a new container from an image
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes
```

  context     Manage contexts
  
  debug*      Get a shell into any image or container
  
  desktop*    Docker Desktop commands (Beta)
  
  dev*        Docker Dev Environments
  
  extension*  Manages Docker extensions
  
  feedback*   Provide feedback, right in your terminal!
  
  image       Manage images
  
  init*       Creates Docker-related starter files for your project
  
  manifest    Manage Docker image manifests and manifest lists
  
  network     Manage networks
  
  plugin      Manage plugins
  
  sbom*       View the packaged-based Software Bill Of Materials (SBOM) for an image
  
  scout*      Docker Scout
  
  system      Manage Docker
  
  trust       Manage trust on Docker images
  
  volume      Manage volumes

#### Swarm Commands:
  
  config      Manage Swarm configs
  
  node        Manage Swarm nodes
  
  secret      Manage Swarm secrets
  
  service     Manage Swarm services
  
  stack       Manage Swarm stacks
  
  swarm       Manage Swarm


#### Commands:

  attach      Attach local standard input, output, and error streams to a running container
  
  commit      Create a new image from a container's changes
  
  cp          Copy files/folders between a container and the local filesystem
  
  create      Create a new container
  
  diff        Inspect changes to files or directories on a container's filesystem
  
  events      Get real time events from the server
  
  export      Export a container's filesystem as a tar archive
  
  history     Show the history of an image
  
  import      Import the contents from a tarball to create a filesystem image
  
  inspect     Return low-level information on Docker objects
  
  kill        Kill one or more running containers
  
  load        Load an image from a tar archive or STDIN
  
  logs        Fetch the logs of a container
  
  pause       Pause all processes within one or more containers
  
  port        List port mappings or a specific mapping for the container
  
  rename      Rename a container
  
  restart     Restart one or more containers
  
  rm          Remove one or more containers
  
  rmi         Remove one or more images
  
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  
  start       Start one or more stopped containers
  
  stats       Display a live stream of container(s) resource usage statistics
  
  stop        Stop one or more running containers
  
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  
  top         Display the running processes of a container
  
  unpause     Unpause all processes within one or more containers
  
  update      Update configuration of one or more containers
  
  wait        Block until one or more containers stop, then print their exit codes

#### Global Options:
  
      --config string      Location of client config files (default
                           "C:\\Users\\Administrator\\.docker")
 
  -c, --context string     Name of the context to use to connect to the
                           daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  
  -D, --debug              Enable debug mode
  
  -H, --host list          Daemon socket to connect to
  
  -l, --log-level string   Set the logging level ("debug", "info",
                           "warn", "error", "fatal") (default "info")
  
      --tls                Use TLS; implied by --tlsverify
      
      --tlscacert string   Trust certs signed only by this CA (default
                           "C:\\Users\\Administrator\\.docker\\ca.pem")
      
      --tlscert string     Path to TLS certificate file (default
                           "C:\\Users\\Administrator\\.docker\\cert.pem")
      
      --tlskey string      Path to TLS key file (default
                           "C:\\Users\\Administrator\\.docker\\key.pem")
      
      --tlsverify          Use TLS and verify the remote
  
  -v, --version            Print version information and quit

Run 'docker COMMAND --help' for more information on a command.
