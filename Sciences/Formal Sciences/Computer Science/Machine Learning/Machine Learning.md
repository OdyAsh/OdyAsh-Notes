
# MLOps

Overview of MLOps flow:
* Model saving & loading
* API
* Docker
* Cloud deployment

## Model Saving and Loading

Why save models:
* Save re-training time
* create multiple versions of the model
* Use model in different environments
* Use models created by others

Types of saving files:
* PMML (allows saving/loading models to/from other programming languages)
* JSON
* Joblib
* Pickle



## API Basics

Analogy: application <-> API <-> backend

* Stands for application programming interface
* It is an interface that allow applications or even components of the same application to communicate and interact with each other
* Communication is done using a set of definitions and protocols (ex: HTTP)
* Could be free or not
* Popular examples: ChatGPT, Google API, Facebook API, etc.
* Can be accessed via:
	* Browser
	* Programming language
	* Command line in terminal (curl)
	* API platform (e.g., postman)
		* Postman is an API platform for building and using APIs.
		* Postman simplifies each step of the API lifecycle and streamlines collaboration so you can create better APIs.
		* Can be used for:
			* API design
			* API documentation
			* **API testing**
			* Mock servers
			* Monitors
			* API detection (in your browser)
		* Generally, the ML team communicates with the front-end team about the structure of the passed JSON to/from the API.
* Types of endpoints (APIs):
	* SOAP APIs
	* RPC APIs
	* Websocket APIs
	* REST APIs
		* Stands for REpresentational State Transfer
		* Most popular/flexible APIs found on the web today
		* ML usually uses this REST API
		* REST API flow: 
		* client sends a **request** (request line, header, body, etc.) to the server.
		* server sends **response** (status line, headers, body, etc.) back to client 
			* "status line" is the "status code" that the server responds with. For example, "400" and "200" corresponds to error and success in the response respectively.


## Python in MLOps

Popular frameworks in Python:
* Flask
* FastAPI
	* Relatively simple
* Django
	* More complex
* Streamlit

### Flask

* Easily implements web applications
* Unlike Django, it is very Pythonic
* Handles low-level details
* Flexible
* Considered a micro-framework


## Docker

* Docker is an open-source containerization platform that revolutionizes software deployment by enabling developers to package applications and their dependencies into lightweight, self-contained, and isolated containers.
* Unlike traditional application deployment methods, Docker provides a consistent and reproducible environment across different machines.

How does it work?:
* It is an API.
* Docker listens on the port that you configured your container with.
* Docker run/build/pull commands are listened/received by the Docker daemon, then the daemon operates on the images/containers based on the listened command.
* docker daemon is like the "server" in the REST API framework.
*  The Docker Engine executes the steps found in the dockerfile and executes it.
	* These steps define the image to be built. A container can be then created and run from this image.
* Docker images are typically stored in a registry (i.e., market place), such as Docker Hub or a private registry.
* OOP analogy: "image" is like a class, "container" is like an object
* "image" is like a blueprint, "container" is like the tangible implementation of that "image".
* Containers:
	* Leverage the host system's kernel.
		* Unlike virtual machines, which require their own operating system kernel.
	* Can be managed via the Docker Engine API or the docker client.
	* Can communicate 
	* Kubernates allow different containers to communicate with each other via orchestration.
* In a dockerfile, the "ENTRYPOINT" (e.g., "python") is what will executes the commands in "CMD" (e.g., "--version", so full example will be "python --version")

### Virtual Machine vs Docker Containers

Docker advantages:
* Resource efficiency
	* Virtual machines require a full operating system to run each instance where docker containers share the host operating system, reducing resource consumption.
* Portability
	* Virtual machines encapsulate an entire OS and application stack making it its size very big, while containers are platform-independent, so it can be run on any system with docker installed.
* Performance
	* VMs have a slight performance overhead due to the abstraction layer between the guest and host OS while docker containers have minimal performance overhead since they can directly work on the host OS, leveraging its kernel

In detail: VM - Containers:
* Hardware-level process isolation - OS level process isolation
* Each VM has a separate OS - Each container can share OS
* Ready-made VMs are difficult to find - pre-built docker containers are easily available
* **VMs can move to new host easily** - docker container has to be deleted, then re-created with the new specifications.
* **VMs have additional security**, as the containers share the same kernel, so if someone were able to find vulnerabilities in the OS level, they can access other containers. - Containers are less secure than VMs.
* VMs boot in minutes - Containers boot in seconds
* VMs use more resources - Containers use less resources
* VMs are a few GBs - Containers are lightweight (KBs/MBs)

## Cloud Deployment

### Cloud vs On-Premise

Cloud - on-remise:
* Pricing: monthly subscription - one-time investment
* Data access: access only via CFM API/connectors - complete access
* Storage: 5GB (extra 2.5GB for every 20 licenses) - limited to available server storage
* Maintenance costs: None - equal to server maintenance cost
* Deployment: fast and simple - complicated, as it requires physical installations
* Up time: 99% uptime but rely on internet connectivity - do not rely on internet to access CRM

Steps to deploy dockerized flas app on AWS using ECS and ECR:
* Create an ECR (Elastic Container Registry) repository to store the image.
	* ECR is like Docker Hub; it is where we push the Docker image.
* Push the Flask application image to ECR repository.
* Create an ECS (Elastic Container Service) cluster.
	* ECS is what we run the docker container on.
* Set up an EC2 instance.
* Deploy and then run the app.

## MLOps and DevOps

DevOps:
* Responsible for automating deployment/testing/maintenance efforts, so that programmers can focus on the project's functionalities/code.
	* Example, when a new feature is developed, the process of deploying/testing this feature is automated; this automation is called CI/CD (Continuous Integration / Continuous Deployment).

MLOps:
* We need MLOps to:
	* work with largescale projects
	* track ML experiments and data history
	* reduce time of delivery
	* reduce human errors
	* reproduce ML experiments
	* Documentation
* Tools include:
	* Git
	* docker
	* Apache Airflow
		* Can schedule based on DAGs (Directed Acyclic Graphs)
	* MLFlow
		* Tracks ML experiments
	* DVC
		* Similar to git, but for data.
	* Terraform
		* Automates the cloud-related steps by writing configuration file (.yaml file) that automates these cloud steps (e.g., AWS steps of creating EC2 instance, etc.)
	* Jenkins

Interesting info:
* When a new feature/model gets deployed, it runs on certain devices, so that if a bug is found, the feature can be roll-backed easily.

## Interview Tips

* Regarding the CV, make sure to emphasize keywords regarding the job description
	* For example, sometimes HR only chooses CVs that contained "AWS" and "time-series".
* Often, you'll get asked about tools more than ML theory (i.e., model types, etc.)
* The most required skills over all interview types/disciplines: **soft skills**
* Regarding technical skills:
	* If 2 people have great soft skills, the person who has knowledge about more tools that are required for the job position will probably be chosen.
* Interviews start with basic questions (e.g., python related questions), then drill down to more detailed topics (e.g., what is Jenkins? etc.)

### HR Behavioral Questions

Usually found on assess.sovaonline.com

