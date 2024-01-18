
# Basic Commands
Most are from [this](https://www.linkedin.com/learning/learning-docker-17236240) course.
## docker run
e.g:
![Pasted image 20230722211957](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230722211957.png)
Explanation:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230722212653.png)
Further explanation of what happens under the hood of the "run" command:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230722212833.png)

e.g. 2:
when running a server image, we use this command:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081205.png)
where `run` creates and starts the container and `-d` does NOT attach the current terminal to it; this will enable us to close the server from the same terminal that we've been using.


## docker build
converts dockerfile to a docker image.
Example:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723080822.png)
Note 1: the `--file` (or `-f`) argument should be provided if your dockerfile is not named "dockerfile".
Note 2: the "." at the end tells docker where the "context" is 
(Side note: "context" is the folder containing files that docker will include in its image, so if the entry point script is in the working directory, then we can leave a "." as the path)

Now, that the image is built, we can run it using:
`docker run our-first-image`


## docker exec

![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081458.png)

![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081540.png)

![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081621.png)

## docker stop, rm, and rmi

to gracefully stop a running container:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081737.png)

to instantly stop it (may lead to data loss based on application logic):
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723081750.png)

to remove all Docker containers, both running and stopped, from your system:
`docker ps -aq | xargs docker rm`
Explanation:
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723082036.png)

to remove images (which take more space than containers):
![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723082240.png)

# Theoretical

## Why use Docker

[amazing source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/)

* Facilitates environment setup and management.
	* Previously, people would (usually) do our local development and unit testing on Windows machines, while all other stages were run on Unix systems. ([source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=do%20our%20local%20development%20and%20unit%20testing%20on%20Windows%20machines%2C%20while%20all%20other%20stages%20were%20run%20on%20Unix%20systems.))
* Solves the problems of 
	* Having identical environments across various stages of development.
	* Having isolated environments for your individual applications.
* Docker uses **containerization** to solve this.

## Containers (Containerization)

Regarding containerization: 
*  It means your application runs in an isolated container
	* This container is an explicitly defined, reproducible and portable environment.
* Containers are immutable. ([source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=you%20can%20stop,new%20runtime%20parameters.))
	* If you want to change the runtime parameters of a container (e.g., `-p 80:80`, you’ll have to stop the container and remove it. Then you need to create a new container from the image with new runtime parameters.
* Containers are stateless ([source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=to%20our%20terminal.-,Data%20in%20Docker%20containers,-Now%20that%20we)).
	* This means that they are reproduced exactly as they were defined and they don’t carry any information with them from any runtime.
	* If you stop and restart your container your data will still be there. 
	* But, if you stop and remove your container to start it with new parameters your data will be lost.
	* To mitigate this, we can share **volumes** (meaning data volumes) between the host and the container. ([source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=we%20can%20share%20volumes%20(meaning%20data%20volumes)%20between%20the%20host%20and%20the%20container.))
		* This keeps the container's data outside of the container, but on the host machine instead.
		* Side note: the mentioned [source](<https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=we%20can%20share%20volumes%20(meaning%20data%20volumes)%20between%20the%20host%20and%20the%20container.>) above talks about volumes, yet the commands that the source's author runs probably run [bind-mount type](https://docs.docker.com/storage/bind-mounts/), not [volume type](https://docs.docker.com/storage/volumes/), as we need to store the data under `$HOME/docker/volumes/` if we’re using Mac or Linux, and `C:\ProgramData\docker\volumes` if we’re on Windows. Otherwise, Docker won’t treat or manage our data as a volume. ([source](https://blog.logrocket.com/docker-volumes-vs-bind-mounts/#:~:text=You%20must%20store%20the%20data%20under%20%24HOME/docker/volumes/%20if%20you%E2%80%99re%20using%20Mac%20or%20Linux%2C%20and%20C%3A%5CProgramData%5Cdocker%5Cvolumes%20if%20you%E2%80%99re%20on%20Windows.%20Otherwise%2C%20Docker%20won%E2%80%99t%20treat%20or%20manage%20your%20data%20as%20a%20volume.))
			* Note about using bind-mount vs volume types: the only advantage of using bind-mount is that it can be accessed and modified by processes outside Docker. ([source](https://blog.logrocket.com/docker-volumes-vs-bind-mounts/#:~:text=You%20must%20store%20the%20data%20under%20%24HOME/docker/volumes/%20if%20you%E2%80%99re%20using%20Mac%20or%20Linux%2C%20and%20C%3A%5CProgramData%5Cdocker%5Cvolumes%20if%20you%E2%80%99re%20on%20Windows.%20Otherwise%2C%20Docker%20won%E2%80%99t%20treat%20or%20manage%20your%20data%20as%20a%20volume.))
				* This can be a benefit when you want to integrate Docker with other processes, but it could also cause a headache if you’re concerned with security.

## Docker Images vs Docker Containers

![](Attachments%20-%20Docker%20Basics/Pasted%20image%2020230723082520.png)

## Dockerfile

[source](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=Here%20you%20can,about%20this%20later.)

* A Dockerfile is the file that defines the building steps of image(s). 
	* You can write your own Dockerfile and run it with `docker build` command. Brief side-notes:
		* If you want to build it from scratch, type `FROM scratch` in the Dockerfile.
			* `scratch` is an explicitly empty image on the Docker store that is used to build base images like Alpine, Debian and so on. ([source](https://takacsmark.com/dockerfile-tutorial-by-example-dockerfile-best-practices-2018/#why-and-when-youd-want-to-use-a-dockerfile:~:text=is%20an%20explicitly%20empty%20image%20on%20the%20Docker%20store%20that%20is%20used%20to%20build%20base%20images%20like%20Alpine%2C%20Debian%20and%20so%20on.))
		* The image you start from is called the **base image**.
	* It doesn't have an extension.
* The directory where you issue the `docker build` command is called the **build context**. ([source](https://takacsmark.com/dockerfile-tutorial-by-example-dockerfile-best-practices-2018/#why-and-when-youd-want-to-use-a-dockerfile:~:text=The%20directory%20where%20you%20issue%20the%20docker%20build%20command%20is%20called%20the%20build%20context))
* In a Dockerfile, you specify the OS (e.g., a Linux distribution like Alpine, which is very lightweight in its storage size) you want to setup.
* [great article](https://takacsmark.com/getting-started-with-docker-in-your-project-step-by-step-tutorial/#:~:text=what%20does%20this,should%20see%20this%3A) that explains port mappings in Dockerfile (e.g., `80:80`)
* The process of creating an image from a Dockerfile is called **building**.
* <mark style="background: #FF5582A6;">Every build step in your Dockerfile will create a new layer in your image</mark>.
	* Think of layers as snapshots on top of each other. If there is a change in a layer, the image will only rebuild starting from that layer and building every consecutive layer. The layers below the changed layer will remain intact. This is called **layer caching**.
	* The term "**intermediate image**" is often used interchangeably with **layers**, [with very few differences between the two](https://vsupalov.com/docker-image-layers/#:~:text=Each%20layer%20is%20an%20image%20itself%2C%20just%20one%20without%20a%20human%2Dassigned%20tag.%20They%20have%20auto%2Dgenerated%20IDs%20though.). 
		* Therefore, **image caching** is often used interchangeably with **layer caching**, [with very few differences between the two](https://medium.com/peak-product/whale-of-a-time-with-docker-6c01c000b5b4#:~:text=Image%20caching%20vs%20Layer%20caching). 
	* Dockerfile instructions create layers to improve build performance.
	* **note that each layer only stores the differences compared to the underlying layer.** ([source](https://takacsmark.com/dockerfile-tutorial-by-example-dockerfile-best-practices-2018/#why-and-when-youd-want-to-use-a-dockerfile:~:text=note%20that%20each%20layer%20only%20stores%20the%20differences%20compared%20to%20the%20underlying%20layer.))
	* A Docker image (even **intermediate** ones) is internally a pointer to the final **layer** of a series of connected layers. ([source](https://stackoverflow.com/questions/60791832/whats-the-docker-intermediate-layer-or-image#:~:text=The%20Docker%20image%20format,specific%20layer%20a%20name)) ([another great source](https://vsupalov.com/docker-image-layers/#:~:text=An%20Image%20Is%20Basically%20A%20Diff))
* 


### Choosing an OS (Distro) for Images

[source](https://kuberty.io/blog/best-os-for-docker/)