## Docker Custom Images Creation Manual

```
PS E:\> docker images
REPOSITORY         TAG       IMAGE ID       CREATED       SIZE
amitkkc01/ubuntu   latest    3f0698943ff5   2 hours ago   297MB
PS E:\> docker run -d --name dkc1345 -p 8990:80 amitkkc01/ubuntu
72bac0edc0366f7daf0cb7747aa064c064fd7510bb37161f2a2963e90e275a36
PS E:\> docker ps 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS E:\> docker ps -a
CONTAINER ID   IMAGE              COMMAND       CREATED          STATUS                      PORTS     NAMES
72bac0edc036   amitkkc01/ubuntu   "/bin/bash"   29 seconds ago   Exited (0) 26 seconds ago             dkc1345
PS E:\> docker run -d --name dkc1345 -it -p 8991:80 amitkkc01/ubuntu
docker: Error response from daemon: Conflict. The container name "/dkc1345" is already in use by container "72bac0edc0366f7daf0cb7747aa064c064fd7510bb37161f2a2963e90e275a36". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
PS E:\> docker run -d --name dkc134567 -it -p 8992:80 amitkkc01/ubuntu
98bf41c24253870e160cfddceb946d8aa087b0acedbf74c79814373eaf1d0da7
PS E:\> docker ps -a
CONTAINER ID   IMAGE              COMMAND       CREATED              STATUS                          PORTS                          NAMES
98bf41c24253   amitkkc01/ubuntu   "/bin/bash"   4 seconds ago        Up 4 seconds                    22/tcp, 0.0.0.0:8992->80/tcp   dkc134567
72bac0edc036   amitkkc01/ubuntu   "/bin/bash"   About a minute ago   Exited (0) About a minute ago                                  dkc1345
PS E:\> 
 *  History restored 

PS E:\DevOps Notes\my_codes> cd..
PS E:\DevOps Notes\my_codes> cd..
PS E:\DevOps Notes\my_codes> cd..
PS E:\DevOps Notes> cd..
PS E:\> git
git : The term 'git' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that
the path is correct and try again.
At line:1 char:1
+ git
+ ~~~
    + CategoryInfo          : ObjectNotFound: (git:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS E:\>
 *  History restored 

usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
           [--work-tree=<path>] [--namespace=<name>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   restore    Restore working tree files
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   diff       Show changes between commits, commit and working tree, etc
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   backfill   Download missing objects in a partial clone
   branch     List, create, or delete branches
   commit     Record changes to the repository
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   reset      Reset current HEAD to the specified state
   switch     Switch branches
   tag        Create, list, delete or verify a tag object signed with GPG
   fetch      Download objects and refs from another repository
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
PS E:\> mkdir Docker

    Directory: E:\


Mode                 LastWriteTime         Length Name                                                                                                                                 
----                 -------------         ------ ----                                                                                                                                 
d-----        09-03-2025     00:12                Docker                                                                                                                               


PS E:\> ls


    Directory: E:\


Mode                 LastWriteTime         Length Name                                                                                                                                 
----                 -------------         ------ ----                                                                                                                                 
d-----        07-03-2025     20:23                DevOps Notes                                                                                                                         
d-----        09-03-2025     00:12                Docker                                                                                                                               
d-----        31-01-2025     21:10                English_Speaking                                                                                                                     
d-----        30-11-2024     23:15                Softwares                                                                                                                            
d-----        30-11-2024     23:55                VMs


PS E:\> cd docker
PS E:\docker> git https://github.com/Empty-Hacker/Netflix-Clone.git
git: 'https://github.com/Empty-Hacker/Netflix-Clone.git' is not a git command. See 'git --help'.
PS E:\docker> git clone https://github.com/Empty-Hacker/Netflix-Clone.git
Cloning into 'Netflix-Clone'...
remote: Enumerating objects: 97, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 97 (delta 4), reused 2 (delta 2), pack-reused 86 (from 1)
Receiving objects: 100% (97/97), 1.29 MiB | 1.46 MiB/s, done.
Resolving deltas: 100% (26/26), done.
PS E:\docker> git --help
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
           [--work-tree=<path>] [--namespace=<name>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   restore    Restore working tree files
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   diff       Show changes between commits, commit and working tree, etc
   grep       Print lines matching a pattern
   show       Show various types of objects

grow, mark and tweak your common history
   branch     List, create, or delete branches
   merge      Join two or more development histories together
   reset      Reset current HEAD to the specified state
   tag        Create, list, delete or verify a tag object signed with GPG

   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
PS E:\docker> docker pull ubuntu/nginx
Using default tag: latest
latest: Pulling from ubuntu/nginx
51a45c9c1b48: Pull complete
5ae9e1fecce9: Pull complete
ec4a38549daa: Pull complete
1dd1ef4e16bd: Pull complete
Digest: sha256:e7a0849d59f24a1fc09cc2bf6f2254d9a7f236b0303541642aec435005d4a32a
Status: Downloaded newer image for ubuntu/nginx:latest
docker.io/ubuntu/nginx:latest
PS E:\docker> docker run -d -name raj23 -it ubuntu/nginx
unknown shorthand flag: 'n' in -name
PS E:\docker> docker run -d --name raj23 -it ubuntu/nginx
eac7806afdf160d0c4d4d9c502c598c2181f6abd77847704f79d8160766d1d60
PS E:\docker> docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
eac7806afdf1   ubuntu/nginx   "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   80/tcp    raj23
PS E:\docker> docker rm raj23
PS E:\docker> docker rm raj23 --force
raj23
e69e7e398538387d97d8e358056a6bb111045bf06fc8b277b6ae36d762a354c6
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
e69e7e398538   ubuntu/nginx   "/docker-entrypoint.…"   5 seconds ago   Up 3 seconds   0.0.0.0:9999->80/tcp   raja23
PS E:\docker> docker cp --help

Usage:  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
        docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
Copy files/folders between a container and the local filesystem

Use '-' as the source to read a tar archive from stdin
and extract it to a directory destination in a container.
Use '-' as the destination to stream a tar archive of a
container source to stdout.

Aliases:
  docker container cp, docker cp

  -L, --follow-link   Always follow symbol link in SRC_PATH
  -q, --quiet         Suppress progress output during copy. Progress
                      output is automatically suppressed if no terminal
                      is attached
PS E:\docker> docker exec -it raja23 bash
root@e69e7e398538:/# cd /var/www/html/
root@e69e7e398538:/var/www/html# cd
root@e69e7e398538:~# ls
root@e69e7e398538:~# ls
root@e69e7e398538:~# exit
exit
PS E:\docker> docker cd . raja23:/var/www/html/
docker: 'cd' is not a docker command.
See 'docker --help'
Successfully copied 2.26MB to raja23:/var/www/html/
root@e69e7e398538:/# cd /var/www/html/
root@e69e7e398538:/var/www/html# ls
Netflix-Clone  index.nginx-debian.html
root@e69e7e398538:/var/www/html# rm -r Netflix-Clone/
root@e69e7e398538:/var/www/html# exit
exit
PS E:\docker> ls


    Directory: E:\docker

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        09-03-2025     00:13                Netflix-Clone


PS E:\docker> cd .\Netflix-Clone\
PS E:\docker\Netflix-Clone> ls


    Directory: E:\docker\Netflix-Clone


Mode                 LastWriteTime         Length Name
d-----        09-03-2025     00:13                images
-a----        09-03-2025     00:13             53 google49bc8e5f8f6b157e.html
-a----        09-03-2025     00:13           5317 README.md
-a----        09-03-2025     00:13           3533 style.css


Successfully copied 2.26MB to raja23:/var/www/html/
root@e69e7e398538:/# ls
bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv 
 sys  tmp  usr  var
root@e69e7e398538:/# cd /var/www/html/
root@e69e7e398538:/var/www/html# ls
README.md  google49bc8e5f8f6b157e.html  images  index.html  index.nginx-debian.html  style.css                                 sys  tmp  usr  var
root@e69e7e398538:/var/www/html# rm index.nginx-debian.html
root@e69e7e398538:/var/www/html# ls
root@e69e7e398538:/var/www/html# exit
exit
PS E:\docker\Netflix-Clone> docker commit --help
Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

Create a new image from a container's changes

Aliases:
  docker container commit, docker commit
Options:
  -a, --author string    Author (e.g., "John Hannibal Smith
  -c, --change list      Apply Dockerfile instruction to the created image
  -m, --message string   Commit message
  -p, --pause            Pause container during commit (default true)
PS E:\docker\Netflix-Clone> docker commit raja23 dkc23/nginx:latest
sha256:83b7a4073d949d7a78e99ed7b1c496bc62ef504ccc4b4691a0d9f9f09ba031b9
PS E:\docker\Netflix-Clone> docker images
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
dkc23/nginx        latest    83b7a4073d94   19 seconds ago   165MB
amitkkc01/ubuntu   latest    3f0698943ff5   3 hours ago      297MB
ubuntu/nginx       latest    1f48792ccb92   8 days ago       163MB
43a0804dc3188cc4f74fa36469868b9cddd7bb4edb9fe7f13ebf2fd84c29d8c9
PS E:\docker\Netflix-Clone> docke ps
docke : The term 'docke' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the     
spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ docke ps
    + CategoryInfo          : ObjectNotFound: (docke:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
 
PS E:\docker\Netflix-Clone> docker ps
e69e7e398538   ubuntu/nginx   "/docker-entrypoint.…"   24 minutes ago   Up 24 minutes   0.0.0.0:9999->80/tcp   raja23
PS E:\docker\Netflix-Clone> docker tag dkc23/nginx:latest dkchcl dineshkc23 latest
"docker tag" requires exactly 2 arguments.
See 'docker tag --help'.

Usage:  docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

PS E:\docker\Netflix-Clone> docker logi
docker: 'logi' is not a docker command.
See 'docker --help'
PS E:\docker\Netflix-Clone> docker login

To sign in with credentials on the command line, use 'docker login -u <username>'

Your one-time device confirmation code is: MHCP-BSJS
Press ENTER to open your browser or submit your device code here: https://login.docker.com/activate

Waiting for authentication in the browser…

Login Succeeded
PS E:\docker\Netflix-Clone> docker tag dkc23/nginx:latest dkchcl dineshkc23 latest
"docker tag" requires exactly 2 arguments.


Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
PS E:\docker\Netflix-Clone> docker images
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
dkc23/nginx        latest    83b7a4073d94   30 minutes ago   165MB
amitkkc01/ubuntu   latest    3f0698943ff5   3 hours ago      297MB
ubuntu/nginx       latest    1f48792ccb92   8 days ago       163MB
PS E:\docker\Netflix-Clone> docker tag 83b7a4073d94 dkchcl/dineshkc23:latest
PS E:\docker\Netflix-Clone> docker push dkchcl/dineshkc23:latest
The push refers to repository [docker.io/dkchcl/dineshkc23]
1f99b22cb72d: Pushed
c2ea87c1216e: Mounted from ubuntu/nginx
8c219a619b58: Mounted from ubuntu/nginx
c8906db992d1: Mounted from ubuntu/nginx
9c8b3e5cca67: Mounted from ubuntu/nginx
latest: digest: sha256:87e44ed9da2e18c4a73e5dd3cd49e97ab7b0e3f6602bdbed4d3a2ba7bd1d58a3 size: 1366
PS E:\docker\Netflix-Clone> docker pull dkchcl/dineshkc23       
Using default tag: latest
latest: Pulling from dkchcl/dineshkc23
Digest: sha256:87e44ed9da2e18c4a73e5dd3cd49e97ab7b0e3f6602bdbed4d3a2ba7bd1d58a3
Status: Image is up to date for dkchcl/dineshkc23:latest
docker.io/dkchcl/dineshkc23:latest
PS E:\docker\Netflix-Clone> docker pull dkchcl/dineshkc23
Using default tag: latest
latest: Pulling from dkchcl/dineshkc23
51a45c9c1b48: Pull complete
5ae9e1fecce9: Pull complete
ec4a38549daa: Pull complete
1dd1ef4e16bd: Pull complete
cacb8935dcbb: Pull complete
Digest: sha256:87e44ed9da2e18c4a73e5dd3cd49e97ab7b0e3f6602bdbed4d3a2ba7bd1d58a3
Status: Downloaded newer image for dkchcl/dineshkc23:latest
docker.io/dkchcl/dineshkc23:latest
PS E:\docker\Netflix-Clone> docker run -d --name raju1234987 -it -p 4546:80 dkchcl/dineshkc23
e1f06c4bdab6c29c4b3385c1f8da1c5ffaaa9878726fadcd91080d1db225afb4
PS E:\docker\Netflix-Clone> docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS                  NAMES
e1f06c4bdab6   dkchcl/dineshkc23   "/docker-entrypoint.…"   16 seconds ago   Up 13 seconds   0.0.0.0:4546->80/tcp   raju1234987
```
PS E:\docker\Netflix-Clone> 
