
# Basic Commands
Most are from [this](https://www.linkedin.com/learning/learning-docker-17236240) course.
## docker run
e.g:
![Pasted image 20230722211957](../../Media/Default/Pasted%20image%2020230722211957.png)
Explanation:
![Pasted image 20230722212653](../../Media/Default/Pasted%20image%2020230722212653.png)
Further explanation of what happens under the hood of the "run" command:
![Pasted image 20230722212833](../../Media/Default/Pasted%20image%2020230722212833.png)

e.g. 2:
when running a server image, we use this command:
![Pasted image 20230723081205](../../Media/Default/Pasted%20image%2020230723081205.png)
where `run` creates and starts the container and `-d` does NOT attach the current terminal to it; this will enable us to close the server from the same terminal that we've been using.


## docker build
converts dockerfile to a docker image.
Example:
![Pasted image 20230723080822](../../Media/Default/Pasted%20image%2020230723080822.png)
Note 1: the `--file` (or `-f`) argument should be provided if your dockerfile is not named "dockerfile".
Note 2: the "." at the end tells docker where the "context" is 
(Side note: "context" is the folder containing files that docker will include in its image, so if the entry point script is in the working directory, then we can leave a "." as the path)

Now, that the image is built, we can run it using:
`docker run our-first-image`


## docker exec

![Pasted image 20230723081458](../../Media/Default/Pasted%20image%2020230723081458.png)

![Pasted image 20230723081540](../../Media/Default/Pasted%20image%2020230723081540.png)

![Pasted image 20230723081621](../../Media/Default/Pasted%20image%2020230723081621.png)

## docker stop, rm, and rmi

to gracefully stop a running container:
![Pasted image 20230723081737](../../Media/Default/Pasted%20image%2020230723081737.png)

to instantly stop it (may lead to data loss based on application logic):
![Pasted image 20230723081750](../../Media/Default/Pasted%20image%2020230723081750.png)

to remove all Docker containers, both running and stopped, from your system:
`docker ps -aq | xargs docker rm`
Explanation:
![Pasted image 20230723082036](../../Media/Default/Pasted%20image%2020230723082036.png)

to remove images (which take more space than containers):
![Pasted image 20230723082240](../../Media/Default/Pasted%20image%2020230723082240.png)

# Theoretical

## Docker Images vs Docker Containers

![Pasted image 20230723082520](../../Media/Default/Pasted%20image%2020230723082520.png)