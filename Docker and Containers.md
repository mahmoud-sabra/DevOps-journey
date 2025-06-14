-## Understanding the Basics and History

## Agenda

- **Containers**
- **Container VS Virualization**
- **Install docker**
- **Simple docker commands**


**Containers** are lightweight, portable units that bundle an application and its dependencies to ensure consistency across different environments.

## 1️⃣ Introduction to Virtualization
### Definition
Virtualization is the creation of a virtual version of physical resources like hardware, operating systems, storage, or networks. It enables multiple independent environments to run on a single physical system. 

### Historical Milestones
- **1960s**: IBM introduced virtualization in mainframe systems, allowing multiple operating systems to run on the same hardware. https://www.ibm.com/topics/virtualization
- **1980s**: With personal computers becoming popular, early hypervisors were developed for research and testing.
- **1990s**: VMware revolutionized IT with the first commercial hypervisor, allowing businesses to consolidate their servers.
- **2000s**: Virtualization became standard in data centers, forming the backbone of cloud services.

### Virtualization Technologies
- **Hypervisors**: The key technology behind virtualization.
  - **Type 1 (Bare-metal)**: Runs directly on hardware without a host OS. Examples:
    - VMware ESXi
    - Microsoft Hyper-V
  - **Type 2 (Hosted)**: Runs on top of a host OS. Examples:
    - VirtualBox
    - VMware Workstation

### Benefits of Virtualization
- **Improved Hardware Utilization**: Run multiple virtual machines (VMs) on a single physical server.
- **Isolation**: Each VM operates independently, improving security and stability.
- **Scalability**: Easily add or remove VMs as needed.
- **Support for Legacy Applications**: Run outdated OS versions or software on modern hardware.

---

## 2️⃣ Introduction to Containers
### Definition
Containers are lightweight, portable units that bundle an application and its dependencies to ensure consistency across different environments.

### Historical Milestones
- **1979**: Unix introduced the `chroot` system call, which isolated a process's file system, a precursor to containers.
- **2008**: Linux Containers (LXC) provided OS-level virtualization, enabling lightweight environments.
- **2013**: Docker introduced an easy-to-use platform for creating and managing containers, simplifying adoption.
- **Present**: Containers dominate modern application development, with tools like Kubernetes orchestrating containerized applications at scale.

### Benefits of Containers
- Lightweight and fast.
- Ensures consistent environments across development, testing, and production.
- Portable across different platforms.

---

## 3️⃣ Virtualization vs. Containers
### Key Differences
| Feature         | Virtual Machines (VMs)                   | Containers                             |
| --------------- | ---------------------------------------- | -------------------------------------- |
| **Isolation**   | Full hardware emulation; separate OS.    | Shares host OS; lightweight isolation. |
| **Performance** | Resource-intensive (each VM has its OS). | Faster and efficient (OS-level).       |
| **Size**        | Large (gigabytes).                       | Small (megabytes).                     |
| **Boot Time**   | Slower (minutes).                        | Faster (seconds).                      |
| **Portability** | Less portable (hardware/OS dependency).  | Highly portable (consistent runtime).  |
| **Use Cases**   | Legacy apps, multiple OS environments.   | Microservices, cloud-native apps.      |

---

## 4️⃣ Choosing Virtualization vs. Containers
### When to Use Virtual Machines
- Running multiple operating systems on a single machine.
- Legacy applications that need complete hardware isolation.
- High-security environments where full OS isolation is required.

### When to Use Containers
- Building microservices and cloud-native applications.
- CI/CD pipelines for rapid development and testing.
- Deploying lightweight, portable applications at scale.

---


- VM template and Runinnig VM
- Containers and images
#### **What Is an Image?**

- A image is a lightweight, stand-alone, executable package that includes:
    - The application code.
    - Runtime environment.
    - System tools, libraries, and dependencies.
- It's like a **snapshot** or **blueprint** for creating containers
  
  **Images Can Be Updated**:
- Use `docker commit` to save changes made in a container to a new image.
#### **What Is a Container?**

- A  container is the **runtime instance** of an image. It is created from an image using the `docker run` command.
- A container:
    - Adds a writable layer over the image, allowing temporary changes.
    - Is isolated, with its own filesystem, network, and resources.



### **What Is Docker?** 🐳

Docker is an open-source platform that simplifies the development, deployment, and management of applications by using **containers**. Containers are lightweight, portable, and efficient, making them ideal for modern software development workflows.
Installation: https://docs.docker.com/engine/install/ubuntu/

Post install: https://docs.docker.com/engine/install/linux-postinstall/

play with docker: [Play with Docker](https://labs.play-with-docker.com/)



## Basic Docker Commands

**Check Docker Version**:
```
docker --version
```


**Pull an Image**:
```
docker pull image_name 
```

**List docker images**
```
docker images 
```

```
docker image ls
```
**Remove an Image**:

```
docker rmi <image_name_or_id>
```




examples:

```
docker pull fedora
```
Create container from image
```
docker container create -it fedora bash
```
Start the container
```
docker container start -i container_namae or container_ID
```
remove container 
```
docker container rm container_name or container_ID
```

simple command 
```
docker container run -it python
```


Container is an application not a virual machine

```
docker container run -it python /bib/bash
```

![[Pasted image 20241127202902.png]]








![[Pasted image 20241127202911.png]]









![[Pasted image 20241127202932.png]]




## Docker Image
```
- A unit of packaging that contains everything required for an application to run

- Application code

- Application dependencies

- OS Constructs
```


```
- In VM analogy an image is like a template VM (Stopped VM)

- Get an image by "Pulling" it from a registry. By default Docker Hub is used

- Consists of layers stacked on top of each other
```

- Images are considered _build-time_ constructs where containers are _runtime_ constructs.
![[Pasted image 20241130152216.png]]
ImageName: Repo:Tag

pull image from unofficial source acountname/repo:tag

Docker Image pull ImageName:latest
![[Pasted image 20241130152236.png]]


docker commands
**Pull an Image**:
```
docker pull image_name 
```

**List docker images**
```
docker images 
```

```
docker image ls
```
**Remove an Image**:

```
docker rmi <image_name_or_id>
```

List Containers
```
docker ps 
```
Stop Container
```
docker stop <container-id>
```
Remove container
```
docker rm <container-id>
```
details about container
```
docker inspect <container-id>
```

Copy From host to container
```

docker cp <source_path_on_host> <container_name_or_id>:<destination_path_in_container>
```
add container name
```
docker container run -d --name NAME imagename
```

## **Docker Network**

### **A. Bridge Network (Default for Containers)**

#### **Use Case**: Containers communicate within the same Docker host.
### **B. Host Network**

#### **Use Case**: Use the host’s network stack directly. Ideal for performance-intensive applications like monitoring tools.
```
docker run --name web -p 8080:80 nginx

```

```
docker run --name web1  --network host nginx 
```
### **C. None Network**

#### **Use Case**: Complete isolation; no networking at all.
```
docker run --name web2  --network none nginx 
```



-------
Examples:

to be done: 

- List all images you have.
- pull image hello-world and run it.
- run 3 nginx containers names web1, web2, web3 to port 8000,8001,8002 and inspect information.
- list all containers running then remove web3.
- create file with content "Hello From Host" and copy it to web3 at /home dir.
- list all network adapters
- make web1 listen to bridge and web3 listen to host
- run python container with bridge network and try to get content of web1 from it
- pull more than python image with different tags and show the difference on layers.
- create container from python called python1 
- try to remove python image used to create the container
- on the container web1 edit content on /user/share/nginx/html/index.html to ```
> <h1>Hello from Nginx!</h1>  then restart the container --> give me the output
 - install vim into web1 and try to take snapshot from container named myimage means[make image from it]
- try tp push myimage to dockerhup.


Session 4 :


create network and connect 


```
docker network create
```

```
docker network connect networkname container
```

task: 
```
create a new network named mycustom_netwok and connect two containers to it (use image you want)
create another network called different_one and connect one container to it (use image you want)
try to ping from one container to the second (in the same network)
try to ping from container to different container (in different network)
```



volumes 
docker cp file1 to /home/
```
docker run -dit --name my_container -v my_volume:/home python
```

bindmount and volume

```
docker volume create my_volume
docker run -dit --name my_container -v my_volume:/app nginx

```
task
```
create new volume and add data to it
run two containers usaing the same volume and read the data from them
```


build your own image 

```
task python image
create nginx image
create hello-world image
```

```
https://github.com/nigelpoulton/psweb.git
```


docker file component
```
# 1. Base Image Declaration
FROM ubuntu:20.04

# 2. Maintainer Information {metadata}
LABEL maintainer="you@example.com"
LABEL version="1.0"
LABEL description="An example Dockerfile demonstrating all key components."

# 3. Environment Variables
ENV APP_ENV=production
ENV APP_PORT=8080

# 4. Working Directory
WORKDIR /app

# 5. Copying Files
COPY app.py /app/
ADD config.tar.gz /app/config/

# 6. Running Commands
RUN apt-get update && \
    apt-get install -y python3 curl 
    
# 7. Exposing Ports
EXPOSE 8080

# 8. Entry Point and Command
ENTRYPOINT ["python3", "app.py"]
CMD ["--port", "8080"]

# 9. Volumes
VOLUME /app/data

# 10. User
USER root

# 11. Health Checks
HEALTHCHECK --interval=30s --timeout=5s CMD curl -f http://localhost:${APP_PORT}/health || exit 1

# 12. Arguments
ARG BUILD_VERSION=1.0
RUN echo "Build version: $BUILD_VERSION"

# 13. Comments
# This is a complete example Dockerfile demonstrating all key components

```