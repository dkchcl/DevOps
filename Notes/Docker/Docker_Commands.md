## Docker Commands:

docker --help

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

#### Common Commands:

**1. run**          # Create and run a new container from an image
```powershell
docker run --help
```
Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```powershell
docker run --detach --name dineshold_pc nginx
```
**2. exec**        # Execute a command in a running container
  
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
**3. ps**          # List containers
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
**4. build**       Build an image from a Dockerfile
```
 docker build --help
```
  ```
  Usage:  docker buildx build [OPTIONS] PATH | URL | -
  ```
**5. pull**        Download an image from a registry
```
docker pull --help
```
```
Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
**6. push**        Upload an image to a registry
```
docker push --help
```
```
Usage:  docker push [OPTIONS] NAME[:TAG]
```

**7. images**      List images
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
**8. login**       Authenticate to a registry
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

**9. logout**      Log out from a registry
```
docker logout --help
```
```
Usage:  docker logout [SERVER]
```
Log out from a registry.
If no server is specified, the default is defined by the daemon.  

**10. search**      Search Docker Hub for images
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
**11. version**     Show the Docker version information
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
**12. info**        Display system-wide information
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

 1. ai*         Ask Gordon - Docker Agent

 2.  builder     Manage builds

 3. buildx*     Docker Buildx
  
  
 4. checkpoint  Manage checkpoints
  
 5. compose*    Docker Compose
  
#### **6. container**   Manage containers
```
docker container --help
```
```
Usage:  docker container COMMAND
```
#### Manage containers ---- Commands:

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
**inspect**     Display detailed information on one or more containers
  ```
docker container inspect --help
```
**kill**        Kill one or more running containers
```
docker container kill --help
```
**logs**        Fetch the logs of a container
```
docker container logs --help
```
**ls**          List containers
```
docker container ls --help
```
**pause**       Pause all processes within one or more containers
```
docker container pause --help
```
**port**        List port mappings or a specific mapping for the container
```
docker container port --help
```
**prune**       Remove all stopped containers
```
docker container prune --help
```
**rename**      Rename a container
```
docker container rename --help
```
**restart**     Restart one or more containers
```
docker container restart --help
```
**rm**          Remove one or more containers
```
docker container rm --help
```
**run**         Create and run a new container from an image
```
docker container run --help
```
**start**       Start one or more stopped containers
```
docker container start --help
```
**stats**       Display a live stream of container(s) resource usage statistics
```
docker container stats --help
```
**stop**        Stop one or more running containers
```
docker container stop --help
```
**top**         Display the running processes of a container
```
docker container top --help
```
**unpause**     Unpause all processes within one or more containers
```
docker container unpause --help
```
**update**      Update configuration of one or more containers
```
docker container update --help
```
**wait**        Block until one or more containers stop, then print their exit codes
```
docker container wait --help
```


**7. context**     Manage contexts
```
docker context --help
```
```
Usage:  docker context COMMAND
```
**Manage contexts**

**Commands:**
```
  create      Create a context
  export      Export a context to a tar archive FILE or a tar stream on STDOUT.
  import      Import a context from a tar or zip file
  inspect     Display detailed information on one or more contexts
  ls          List contexts
  rm          Remove one or more contexts
  show        Print the name of the current context
  update      Update a context
  use         Set the current docker context
```

 8. debug*      Get a shell into any image or container
  
 9. desktop*    Docker Desktop commands (Beta)
  
 10. dev*        Docker Dev Environments
  
 11. extension*  Manages Docker extensions
  
 12. feedback*   Provide feedback, right in your terminal!
  
 13. image       Manage images
  
 14. init*       Creates Docker-related starter files for your project
  
 15. manifest    Manage Docker image manifests and manifest lists
  
**16. network:**     - Manage networks
```
docker network --help
```
```
Usage:  docker network COMMAND
```
**Manage networks**

**Commands:**

**a) connect:**     - Connect a container to a network
```
Usage:  docker network connect [OPTIONS] NETWORK CONTAINER
```
Connect a container to a network
```
Options:
      --alias strings           Add network-scoped alias for the container
      --driver-opt strings      driver options for the network
      --ip string               IPv4 address (e.g., "172.30.100.104")
      --ip6 string              IPv6 address (e.g., "2001:db8::33")
      --link list               Add link to another container
      --link-local-ip strings   Add a link-local address for the container
  ```

**b) create:**      - Create a network
```
Usage:  docker network create [OPTIONS] NETWORK
```
Create a network
```
Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by
                             Network driver (default map[])
      --config-from string   The network from which to copy the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge")
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable or disable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a
                             network segment
  ```

**c)  disconnect:**  - Disconnect a container from a network
```
Usage:  docker network disconnect [OPTIONS] NETWORK CONTAINER
```
Disconnect a container from a network
```
Options:
  -f, --force   Force the container to disconnect from a network
```

**d)  inspect:**     - Display detailed information on one or more networks
```
Usage:  docker network inspect [OPTIONS] NETWORK [NETWORK...]
```
Display detailed information on one or more networks
```
Options:
  -f, --format string   Format output using a custom template:
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using the given
                        Go template.
                        Refer to https://docs.docker.com/go/formatting/
                        for more information about formatting output with
                        templates
  -v, --verbose         Verbose output for diagnostics
  ```

**e)  ls:**          - List networks
```
Usage:  docker network ls [OPTIONS]
```
List networks

Aliases:
  docker network ls, docker network list
```
Options:
  -f, --filter filter   Provide filter values (e.g. "driver=bridge")
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
      --no-trunc        Do not truncate the output
  -q, --quiet           Only display network IDs
  ```

**f)  prune:**       - Remove all unused networks
```
Usage:  docker network prune [OPTIONS]
```
Remove all unused networks
```
Options:
      --filter filter   Provide filter values (e.g. "until=<timestamp>")
  -f, --force           Do not prompt for confirmation
```

**g)  rm:**          - Remove one or more networks
```
Usage:  docker network rm NETWORK [NETWORK...]
```
Remove one or more networks

Aliases:
  docker network rm, docker network remove
```
Options:
  -f, --force   Do not error if the network does not exist
```
  
 17. plugin      Manage plugins
  
 18. sbom*       View the packaged-based Software Bill Of Materials (SBOM) for an image
  
 19. scout*      Docker Scout
  
 20. system      Manage Docker
  
 21. trust       Manage trust on Docker images
  
 22. volume      Manage volumes

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
