#Starting OpenDF on docker machine
This document lists steps to get he OpenDF-Web application up and running in a docker managed container.

List available machines in the system
###docker-machine ls

```
NAME      ACTIVE   DRIVER       STATE     URL   SWARM   DOCKER    ERRORS
default   -        virtualbox   Stopped                 Unknown
```

Start the default machine

###docker machine start default

```
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER    ERRORS
default   -        virtualbox   Running   tcp://192.168.99.101:2376           v1.11.2
```

Set up the environment

###docker-machine env

```
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.101:2376"
export DOCKER_CERT_PATH="C:\Users\bishtsum\.docker\machine\machines\default"
export DOCKER_MACHINE_NAME="default"
\#Run this command to configure your shell:
\#eval $("C:\Program Files\Docker Toolbox\docker-machine.exe" env)
```

After this, the docker should be active to start different containers

###$ docker-machine ls

```
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER    ERRORS
default   *        virtualbox   Running   tcp://192.168.99.101:2376           v1.11.2
```

List available containers
###$ docker images

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
my_opendf           latest              227b43d35492        9 days ago          2.225 GB
glassfish           latest              7d04a1452d00        5 months ago        773.3 MB
<none>              <none>              8f41ed926b8d        6 months ago        165.7 MB
node                latest              e3e7156ded1f        6 months ago        652.8 MB
nginx               latest              4efb2fcdb1ab        6 months ago        183.4 MB
mysql               latest              4b3b6b994512        6 months ago        384.5 MB
ubuntu              latest              cf62323fa025        8 months ago        125 MB

...
```

Run the Open DF instance
###$ docker run -p 8080:8080 my_opendf

Verify in the same console (after doing a Ctrl + C) or on a different console

###$ docker ps

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                        NAMES
e6d0d4e09aae        my_opendf           "/bin/sh -c 'asadmin "   2 minutes ago       Up 5 minutes       4848/tcp, 8181/tcp, 0.0.0.0:8080->8080/tcp   condescending_payne
```

#Open browser to reach the login page
(http://192.168.99.100:8080/OpenDF-web)

If mysql is not started and glassfish gives connection errors (500) 

##SSH to container
###docker attach <CONTAINER ID/NAMES>
eg; docker attach e65ddb4273f4

OR run the bash directly
###winpty docker exec -i -t e65ddb4273f4 bash

There, start mysql
####/etc/init.d/mysql start

Now, the application should be up and running.
