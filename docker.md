### [Docker Tutorial](https://www.youtube.com/watch?v=pTFZFxd4hOI&list=PLOEG1MmaatwcG3oPNxP-Pu_yCsB6d4FjX&index=19&ab_channel=ProgrammingwithMosh)

### [Jenkins Tutorial](https://www.youtube.com/watch?v=mk2FBuTMwDc&ab_channel=Simplilearn)

### With docker we can package our application with everythning it needs and run in anywhere in any machine in an isolated environment called container.

    docker-compose up
    docker-compose down --rmi all

### Containers are more lightwright and they share the operating system of the host

### Client uses REST API to communicate with Docker Engine which performs all the tasks

### All containers share the Kernel of the hosts - Hence the container need to be developed for running on particualr operating system
#### PS : Windows can run both windows and linux containers

### Download Docker for windows 
#### Enable Hyper - v for windows (Note : Can't use Hyper-V on Windows 10 Home)
#### Update WSL-2


### Inorder to dockerize an application we need to add dockerfile which contains all the details required for containerizing the application and create an image.

### The container will have it's own filesystem. Hence the application will run inside the container locally.

### Once we create an image, we push it to docker registry/ docker hub. Any machine with docker hub can use this container.

## Development Workflow

### Take an example application app.js
    console.log("Hello Docker!");

#### Inorder to run this application we need to
- Start the OS
- Install Node
- Copy app files
- Run node app.js

### We can wrte these instructions inside dockerfile and automate these processs

### Inorder to do that, create a file named Dockerfile
### Now we need to write this Dockerfile to package our application
- We need to start from base image (Like Inheretence in programming) usnig FROM keyword -- Refer Dockerhub for knowing these image names 
- These node images are built on different linux distributions. We need to specify which linux distribution we want to use
- Now we need to copy all the files into the docker filesystem using COPY keyword
- WORKDIR is used to specify current working directory
- Now we use CMD keyword to specify which command to be executed

    FROM node:alpine
    COPY . /app
    WORKDIR /app
    CMD node app.js
    
### Now inorder to package our application we need to use following commands

    docker build -t <tag> <director>

### The image is not stored in the same directory, infact image file is not a single file.
### To view all the images in the computer, we need to use the command
    docker image ls
    or
    docker images
#### Tags are basically used for versioning of the images

### To run the docker image, execute
    docker run <repository>

### Now we can push the image to dockerhub and use it in any machine by pulling it.
### To understand docker better use this virtual lab [here](https://labs.play-with-docker.com/)


### TO pull the image we use
    docker pull <repositoty-name>

### Docker has it's functionalities built on top of linux

### Basic Linux Commands
#### Different Linux Distributions are
- Ubuntu
- Debian
- Alpine
- Fedora
- CentOs
  
### Learning Ubuntu Distribution
    docker run ubuntu
#### This will auto-pull the image if not found in local system

### To list running containers
    docker ps
### To list all containers
    docker ps -a

### To start container in interactive mode
    docker run -it ubuntu

### Command line 
    echo hello
    whoami
    echo $0

    history
    !2


### Managing packages
### In ubuntu we use apt for managing packages
#### Other package mangers are node, pip etc

### To install local pacakge
    apt install nano

### To download and install a package after updating the package list
    apt update
    apt list
    apt install nano

### To remove a package
    apt remove nano


### Navigating linux file system
    pwd
    ls
    ls -1
    las -l
    cd <dir>
    cd ~
    cd ..

### Manipulating files and directory in the docker containers
    mkdir <dir-name>
    mv <name-1> <name-2>
    cd <name-2>
    touch <file-name> <file2> <file3>
    rm <file-name>
    rm -r <dir-name>

    nano <file-name>
    cat <file-name>
    more <file-name>
    less <file-name>
    
    cat <file1> <file2>  >   <file3>
    ls -l /etc > files.txt
    
<br/>

### [Docker Compose Tutorial](https://www.youtube.com/watch?v=HG6yIjZapSA&list=PLOEG1MmaatwcG3oPNxP-Pu_yCsB6d4FjX&index=24&ab_channel=ProgrammingwithMosh)

### Docker Compose for building and running multi-container applications
### Here we take example of app built using React, Node and MongoDB

### Docker compose is built on top of Docker Engine.
#### [Installation Doc](https://docs.docker.com/compose/install/)
#### No need to install if you use docker desktop

### To remove docker images
    docker image r
    m <image-id>
    
    docker container rm -f $(docker container ls -a -q)
    docker image rm -f $(docker image ls -a -q)

### For composing a multi-conatainer application we use docker-compose.yml

#### We can use migration script to automatically populate data in the database

### json and yml formats

#### data.json
    {
        "name": "The Ultimate Docker Course",
        "price" : 19
        "is_published" true,
        "tags" : ["software", "devops"],
        "author" : {
            "first_name" : "Mosh",
            "last_name" : "Hamedani"
        }
    }

#### data.yml

    ---
     
    name: The Ultimate Docker Course
    price : 19
    is_published true
    tags : 
        - software
        - devops
    author :
        first_name : Mosh
        last_name : Hamedani
    
#### Parsing yml file is slightly slower than parsing json

### Creating compose file from scratch
#### docker-compose.yml
- Version needs to be specifically mentioned as string
- Get the latest version number from [website](https://docs.docker.com/compose/compose-file/)
- Service names can be anything. Here we are specifying how to build these images and how to run these images
- Under build property specify where to find the dockerfile
- Map port of host to port of container using host-port:container-port
- To list all valued properties go to [website](https://docs.docker.com/compose/compose-file/compose-file-v3/)
- We need environment variable to tell where our database is
- We need to define volumes to make sure data is mot stored in container file system, instead stored in host machine

<code>
    version: "3.8"
    services:
        frontend:
            build: ./frontend
            ports:
                - 3000:3000
        backend:
            build: ./backend
            ports:
                - 3000:3000
            environment:
                DB_URL : mongodb://db/appname
        database:
            imageL: mongo:4.0-xenial
            ports:
                - 27017:27017
            volumes:
                - appname: /data/db
    volumes:
        appname:
</code>

### Run this to get all the sub commands
    docker-compose

### Important docker commands 
    docker-compose build --help
    docker-compose build --no-cache
    docker-compose build --pull

### To start an application we use 
    docker-compose up
    docker-compose up -d
    docker-compose up --build

    docker-compose ps
    docker ps

### To stop application
    docker-compose down

### Networking in docker
### When we create docker containers, docker will automatically create network and add the containers to the network

    docker network ls

    docker exec -it -u <id> sh
    $ ping <service-name>
    $ exit

### Docker comes with embedded DNS server. So this DNS server maps IP to the service name

### We access these ports of NAT using port mapping

