---
title: "Building Scalable GO Application With Docker, AWS, and GitHub Actions"
datePublished: Fri Feb 07 2025 21:11:05 GMT+0000 (Coordinated Universal Time)
cuid: cm6v9h0dq000e0al7asep0ntn
slug: building-scalable-go-application-with-docker-aws-and-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738807715646/e6db401e-5c94-4fa0-a4bb-dc06130106d9.png
tags: cloud, programming-blogs, docker, go, backend, developer, beginners

---

# Introduction

* Hey, Gophers! Thanks for stopping by and taking the time to read my blog. If you’ve been following my previous blogs, you might know that I recently started writing about Go. In my last article, we explored JWT authentication using the JWT and Fiber packages in Go.
    
* After covering the basics, I learned more advanced topics, such as working with databases, handling cookies and sessions, deploying Go applications on the cloud, using Docker, containerizing Go applications, etc.
    
* And to put all these concepts into practice, I built a project that combined them all. Honestly, it was quite a challenge since AWS, Dockerization, Redis, and GitHub Actions were new to me. But after overcoming everything, I’m excited to share everything I’ve learned with you.
    
* In this series, I’ll break down each concept in a simple and easy-to-understand way. If anything is unclear, feel free to ask in the comments!
    
* By the end of this series, you’ll have a fully deployed, containerized project running in the cloud. If you're a beginner, this project will be a great addition to your resume, as we’ll be implementing many industry standard practices used in real-world applications.
    
* We first need to learn a very important concept/tool called **Docker.** Because nowadays everyone is using it.
    
* So, let’s first start with Docker and understand what Docker is. Why do we and people in the software industry use it? And What problem does it resolve?
    

---

# Why do we need Docker?

* Before diving into what Docker is, let's first understand the issues it helps to resolve.
    
* Imagine an organization with hundreds of developers, each working on different machines with different operating systems and configurations. Now, consider a project where a team of 50 developers is collaborating on the same GitHub repository.
    
* As the team grows, new developers are hired and provided with new systems to work on. To get started, they need to clone the project from the repository and set up the development environment. Let's take two developers as an example:
    
    * **Developer 1** – A current employee who has already set up the project environment.
        
    * **Developer 2** – A new employee who has just joined and needs to set up the project from scratch.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738801055565/de5f91c4-4db7-47fb-a97c-16f2bd089dcd.png align="center")

* **Developer 1**, who has been working on the project from the beginning, has already set up all the necessary environments. Since this is a Go project, he runs the server locally using the following versions of key dependencies:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738801665997/268d347b-357d-439c-ab9a-7f1048fc92ba.png align="center")
    
* Now, the real challenge begins when **Developer 2** (a new employee) joins the team and needs to run the project on his system.
    
    #### Challenges Faced by the New Developer
    
    1. **Manual Setup Hassle**
        
        * The new developer first clones the project from the repository.
            
        * He then needs to install multiple dependencies manually (Go, MongoDB, Redis, etc.).
            
        * In real-world projects, there are even more dependencies to install, making the setup tedious and error-prone.
            
    2. **Operating System Differences**
        
        * Developer 1 might be using **Windows**, while Developer 2 has a **Mac**.
            
        * Some project commands may work on Windows but not on Mac.
            
        * Certain OS-specific compatibility issues might arise during the setup.
            
    3. **Version Mismatches**
        
        * Developer 2 might install the latest versions of dependencies, which could be **incompatible** with the project.
            
        * Some dependencies may have breaking changes, causing unexpected issues.
            
    4. **Cloud Deployment Challenges**
        
        * Eventually, the project will need to be deployed on the **Cloud**.
            
        * The cloud server might have a different environment, requiring another round of installations and conflict resolution.
            
        * Even after setting everything up, there’s no guarantee that the project will work as expected.
            
    5. **Scalability Issues**
        
        * Today, it’s just one new developer-facing these challenges, but as the team grows, the setup process will have to be repeated for every new team member.
            
        * Constant communication and troubleshooting with each developer become inefficient and time-consuming.
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738801835525/36f07888-4daf-4230-99e4-d0732b620a10.png align="center")
    
    * This is where **Docker** comes into play. It provides a way to package the entire environment, ensuring that everyone (developers and cloud servers) runs the same setup without manual installations or version mismatches.
        
    * In the next section, we’ll dive into **what Docker is, why it is useful, and how it solves these problems**.
        

---

# How does Docker resolve this problem?

## Docker Container

* **Docker is a platform** that allows developers to create, deploy, and run applications inside **containers**.
    
* What is **a Container?**
    
    * You can think of a **container** as a **box** that holds everything needed to run an application: its code, runtime, dependencies (like Go, MongoDB, Redis), and any required configurations.
        
* With Docker, we can create a **container** that includes all the necessary tools, packages, and dependencies. This container ensures that:
    
    * Every developer gets the **exact same versions** of Go, MongoDB, Redis, and other dependencies.
        
    * The application runs **identically on every system.**
        
    * The container is **lightweight**, meaning it doesn’t take up unnecessary resources like a full virtual machine would.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738804258230/afb417c8-8d1d-4214-b825-d3c33a1b5b04.png align="center")

* As you can see, this resolves the very big issue of installing and setting up the project environment again and again, and we can save our developers from the manual errors that they can make, as seen above.
    

> To conclude, With Docker, we don’t have to install things like MongoDB or Redis manually again and again. Instead, we can run them inside containers and start using them instantly!

* Okay, so now that we understand containers, there is one more term that we need to understand, which is Images.
    

---

# Docker Images

* A **Docker image** is like a **recipe** that contains all the necessary ingredients and instructions to prepare a dish. However, instead of food, a **Docker image** contains everything needed to set up and run a software application.
    
    ## Understanding Docker Images with an Example
    
    * Imagine you have a laptop. Without an **operating system** (Windows, Mac, or Linux), your laptop is just a piece of hardware that can’t do much. Similarly, a **Docker container** needs a **Docker image** to function.
        
    * Think of a **Docker image** as the **"operating system"** for a container. It includes:
        
        * The **application code**
            
        * All the **dependencies** (like Go, MongoDB, Redis, etc.)
            
        * The **runtime environment**
            
        * Any necessary **configurations**
            
    * Once a Docker image is created, it serves as a **blueprint** to generate multiple **containers**. Each container runs independently but follows the same instructions defined in the image, just like you can cook the same dish multiple times using the same recipe.
        
    * With Docker images, developers can ensure consistency across different environments, making application deployment seamless and reliable.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738807602410/ce121aa0-db24-4bcb-8aef-cf146af4bf34.png align="center")
    
    * I hope everything is clear now.
        
    * If not, then don’t worry; we are now going to do some hands-on exercises and see everything that we have learned so far in action.
        

---

# Docker Installation

## Docker Desktop

* To run **Docker containers** on your machine, you need to install the **Docker Desktop** application.
    
    You can download it from the official website:
    
* [Docker Desktop Installation](https://www.docker.com/)
    
* Or simply search **“Docker Desktop install”** online, and it will take you to the installation page.
    
* **Docker Desktop** is a **GUI (Graphical User Interface)** that makes it easy to:
    
    * Manage **containers**
        
    * View and control **Docker images**
        
    * Monitor **volumes** and **networks**
        
    * Configure **Docker settings**
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738886863347/3504b267-b621-430f-a1b8-8f572ebaa961.png align="center")

* It provides a user-friendly way to interact with Docker without using only command-line tools, making container management more accessible.
    
* Once you are done with the installation, open the terminal of your choice and run `docker` command
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738887424428/741f9615-ccda-49c0-839e-6a0953f4d2bd.png align="center")

* It should show a similar result. This tells us that docker is successfully installed in our system. You can also verify using.
    

```go
docker --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738887737906/3e9037d6-d66d-4620-b8f5-3da748c9bc59.png align="center")

* Now open your Docker desktop.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738887841617/c17eafdf-db9b-4a44-8337-9f976f355ff3.png align="center")

* If you open **Docker Desktop**, you’ll notice several sections on the left-hand side:
    
    * **Containers** – Shows running and stopped containers.
        
    * **Images** – Lists downloaded and built Docker images.
        
    * **Volumes** – Manages persistent data storage for containers.
        
    * **Builds** – Tracks built images and processes.
        
* We've already covered **Containers** and **Images**, and that’s all we need to get started!
    
* Okay, so for our upcoming project, we’ll need **MongoDB** and **Redis** as dependencies. Instead of **manually installing** them and setting up everything from scratch (which is boring and time-consuming 😩), we can use **Docker** to simplify the process.
    
* With Docker, we can:
    
    * Pull **pre-built images** of MongoDB and Redis.
        
    * Run them as **containers**.
        
    * Avoid dependency conflicts or setup issues.
        
* This means **no more frustrating installations**, we just run a command, and everything works!
    
* Before that, let’s understand what Docker hub is.
    

---

# Docker Hub

* You might be wondering when I say we need to pull Docker images for MongoDB and Redis, where these images actually come from. It comes from Docker Hub. Docker hub is similar to Github but for docker images.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738888750254/59ef5588-7192-4735-934c-9de49613bc84.png align="center")

* It’s an online repository where developers can find and share Docker images.
    
* You can also create your custom image on your system and push it to the docker hub for others to use. We are going to create a custom image for our Go application and push it to the docker hub in the future.
    
* What we, as developers, have to do is just pull these images using the command `docker pull`, and we are all set.
    

---

# Running MongoDB in a Docker Container

* Instead of manually installing MongoDB, we can use **Docker** to set it up in seconds with the following command:
    

```powershell
docker run -d --name mongo-demo \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=admin \
-p 27017:27017
mongo:8.0
```

* Let’s understand this command:
    
    * `docker run -d` : It runs this container in a detached mode. This means that if we do not provide this tag, our terminal will be in use, and we won’t be able to perform any other operations. So, we need to run this container in the background
        
    * `—name mongo-demo` : We are naming our container as ‘mongo-demo’
        
    * Now, for security purposes, we are setting the Username and Password for our database using `-e MONGO_INITDB_ROOT_USERNAME` and `-e MONGO_INITDB_ROOT_PASSWORD`
        
    * We are also mentioning the `port` We want Mongo to run locally in our system.
        
    
    > ## PORT MAPPING
    > 
    > * When we run MongoDB inside a **Docker container**, it operates in an **isolated environment**. This means it **does not**automatically connect to our **local machine**.
    >     
    > * If we try to access MongoDB **from outside the container**, it won’t work unless we **explicitly expose its port**.
    >     
    > * This is where **Port Mapping** comes in!
    >     
    > 
    > Here, `-p 27017:27017` means:
    > 
    > * The first `27017` (before the `:`) is the **port on your local machine** (host).
    >     
    > * The second `27017` (after the `:`) is the **port inside the container**.
    >     
    > 
    > By default, services running **inside a Docker container** are **not accessible** from outside.
    > 
    > * MongoDB **inside the container** is running on **port 27017**.
    >     
    > * But our system (local machine) **doesn’t know that** unless we explicitly expose it.
    >     
    > * By mapping **MongoDB’s internal port (27017) to our system’s port (27017)**, we make it accessible.
    >     
    
    * At the end, we are specifying which image to pull, and that is `mongo:8.0`
        
    * If you search Mongo in the docker hub, you will find its image shown below.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738889210463/8878f7c9-0c9e-437e-9b42-d01f65d206ec.png align="center")
        
* What that above command will do is :
    
    * Pulls the **MongoDB 8.0 image** from Docker Hub (if not already downloaded).
        
    * Starts a **MongoDB container** with a **default admin username and password**.
        
    * Allows us to interact with MongoDB just like we would on a locally installed version, but without the manual setup!
        
* Once it is done, you will see this container running in your Docker Desktop.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738889497178/c0d717fa-f141-42ac-98bd-4451c91cece9.png align="center")

* To check if it’s running or not, you can run the below command
    

```powershell
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738889831317/34e37744-3aee-40ea-8aef-5fe88d886c3d.png align="center")

* This will list all the running containers
    
* Now, let’s run the Redis container
    

---

# Running Redis in Docker Container

* Just like MongoDB, we can set up **Redis** instantly using Docker without manually installing anything. Use the following command:
    

```powershell
docker run -d --name redis-demo redis:latest
```

* This will pull the **latest Redis image** (if not already available locally) and then start a **Redis container** that runs in the background.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738891888914/8ac8bb10-b5fd-4226-9d10-4b364b736d3c.png align="center")
    
* Again, to verify whether it’s running or not, let’s run `docker ps`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738891941701/b5bcb82f-23d4-47ba-84c4-34e9e87d3ea4.png align="center")

* As you can see, our Mongo and Redis containers are working pretty well.
    

> Now that we have **MongoDB and Redis running inside containers**, we don’t need to install them manually on our system. Anytime we need them, we can just **start the containers**, and everything will work instantly.

---

# Wrapping Up

* With Docker, we’ve reduced the hassle of manual installations and ensured a **consistent** and **error-free** development environment. No more dependency issues or version conflicts, just a simple setup in seconds!
    

---

# What’s Next?

* This blog serves as the **foundation** for the next steps in our series. Now that you understand docker and how it works. We are ready to containerize our Go application.
    
* Stay tuned for the next part! 🚀 Until then.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711803084752/aa266313-a315-41a8-9538-8ff4370577fb.gif?auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm align="center")

* Connect with me on [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/)**,** [**Github**](https://github.com/red-star25)**, and** [**Twitter**](https://twitter.com/dhruv_nakum)**.**