## what is difference between images and containers

## what are layers in images

1st file:

FROM node

WORKDIR /app

COPY . /app

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]



2nd file: optimization : since the npm install shouldnt run each time even if only the code is changed thats why we only copy the package json first and then npm i so that this layers are skipped as they are already present in cache and only the code changes are rebuild when we build the image again.

FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

EXPOSE 80

CMD ["node", "server.js"]

omkar2004@omkar-HP-Laptop-15s-fq5xxx:~/Devops/tut1/nodejs-app-first-dockerfile$ docker build .
[+] Building 1.2s (10/10) FINISHED                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                    0.0s
 => => transferring dockerfile: 152B                                                                                                                    0.0s
 => [internal] load metadata for docker.io/library/node:latest                                                                                          0.9s
 => [internal] load .dockerignore                                                                                                                       0.0s
 => => transferring context: 2B                                                                                                                         0.0s
 => [1/5] FROM docker.io/library/node:latest@sha256:a2f09f3ab9217c692a4e192ea272866ae43b59fabda1209101502bf40e0b9768                                    0.0s
 => [internal] load build context                                                                                                                       0.0s
 => => transferring context: 4.39kB                                                                                                                     0.0s
 => CACHED [2/5] WORKDIR /app                                                                                                                           0.0s
 => CACHED [3/5] COPY package.json /app                                                                                                                 0.0s
 => CACHED [4/5] RUN npm install                                                                                                                        0.0s
 => [5/5] COPY . /app                                                                                                                                   0.1s
 => exporting to image                                                                                                                                  0.1s
 => => exporting layers                                                                                                                                 0.0s
 => => writing image sha256:b358e06e5c4796208c4b4d4df180b7ed4ccb3bcd88051872eceec7b8eb51e8b2




 ## learnings
 - using --help effectively you dont need to memorized anything

 -  managing images and containers:
    -   images can be tagged, listed, analyzed, removed
    -   containers can be named, can be configured in detail

 - stopping and restarting containers using docker run container_name

 - attached and detached containers using flags -a, -d, logs, attach etc


# COMMANDS :
1. building image : docker build .
2. running a container : docker run --help
    - docker run -p 3000:80 <image_id>
3. stopping a container :
    - docker stop <container_name>
4. see running containers : 
    - docker ps
5. see all containers (stopped + running):
    - docker ps -a
6. restarting docker container
    - docker start <container_name>
7. attached and detached mode
    - -d, -a
8. attaching to container
    - docker attach <running_container_name>
9. entering docker in interactive mode
    - docker run -i
10. restarting docker container in interactive mode with new terminal
    - docker run -i -t
