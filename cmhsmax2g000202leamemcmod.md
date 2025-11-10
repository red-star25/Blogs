---
title: "Ship It Like a Pro: Node.js on EC2 with Caddy & systemd"
datePublished: Mon Nov 10 2025 04:03:43 GMT+0000 (Coordinated Universal Time)
cuid: cmhsmax2g000202leamemcmod
slug: ship-it-like-a-pro-nodejs-on-ec2-with-caddy-and-systemd
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1762747315634/05e6012f-75a4-4cb8-859b-02276fbd9a0c.gif
tags: ec2, programming-blogs, aws, deployment, nodejs, developer, cloud-computing, amazon-web-services, ubuntu-2204

---

# Introduction

* I've been learning a lot about AWS lately, and to be honest, there's a lot to understand and learn. I decided to take a little break and try to implement what I've learned so far. At the same time, I'm working on a project that's still in progress, and I'll be announcing it soon. I have a backend app in Node.js for this project and wanted to deploy it. So, I thought, why not deploy it on AWS to test my knowledge and see if I've learned anything?
    
* A little bit about my Node.js app: I'm using JavaScript, and I have MongoDB running. It's on Atlas in the cloud. I think that's all you need to know. If you have a Node.js application running, you can follow similar steps to make your backend accessible to your frontend application or any third-party consumer.
    
* So, without further ado, let's get started.
    

---

# Set up an AWS Account

* First, we need an AWS account, so I'm assuming you already have one. If not, it's really easy to create one. Go to [https://aws.amazon.com](https://aws.amazon.com) and create an account.
    
* It might ask for your credit card information, but don't worry, they won't charge you until you exceed the free-tier limit. In this guide, we won't exceed the free tier, so there's no need to worry. Just add your details, and you're all set.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762472741823/3c3cfdd2-3058-49c7-833c-9de1e99fd12b.png align="center")

---

# AWS EC2 Instance

* So, we are going to use the AWS EC2 service to deploy our application to AWS. If you're not familiar with EC2, think of it as renting a virtual machine, similar to your laptop or PC. There are many benefits, such as storing data, choosing your operating system, deciding how much computing power you need, selecting the number of CPU cores, RAM, and the type of network you want to use, and more.
    
* You can customize your virtual machine as you like and rent it from AWS, which is the power of the cloud.
    
* What we'll do is copy our local app, with all its files and folders, directly to this virtual machine and then run the app there. The advantage is that anyone with the link can access it, not just us on our local machine.
    

---

# Creating EC2 Instance

* Simply search for EC2 in the search bar and click on it to open the service page.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762538757575/d7139c10-6121-476e-8c2e-2b815254a19f.png align="center")

* Once it's open, you will see a page like this.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762538803979/d9858efc-b7ed-4b14-9b26-11b259f42605.png align="center")
    
    * Simply click on a Launch Instance on Dashboard and give it a name.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762538890516/d043f510-ab55-4054-96e9-180bf2771294.png align="center")
    
    * It will also ask you to select the operating system image. Choose Ubuntu and scroll down.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762538972299/36e35659-2e56-4fad-ab3a-c8bed8154c77.png align="center")

* We will use the `t2.micro` instance because it is part of the free tier. If you need a higher configuration CPU, you can check other instances and select the one that meets your needs.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539062261/6906a284-e72e-4ef7-b92a-a85da7e982e2.png align="center")

* To connect to the instance from our local machine or anywhere else, we need access. To do this, we generate a key pair, which we can use to connect to our AWS instance and launch it in our local environment.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539188902/2daf408e-9be9-4ded-a7a1-3f6733c94449.png align="center")

* Click on "Generate Key Pair," give it a relevant name, and make sure to select the RSA key pair type. Finally, create the key pair, and it will download to your local machine.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539363601/a6b2c185-9b9d-4fe5-b726-466e2e3a1ac0.png align="center")

* In the network settings, select:
    
    * Allow SSH traffic from - **My IP -** Because we only want to access the instance from our local machine.
        
    * Allow HTTPS traffic from the internet (so our application can access our Node.js server using an endpoint or URL with HTTPS)
        
    * Allow HTTP traffic from the internet (so our application can access our Node.js server using an endpoint or URL with HTTP)
        
* That's it. Now, review the summary and launch the instance.
    

---

# Connecting via SSH

* Once it’s created, click on `Connect to your instance`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539556290/34f5e2ae-0e62-4512-994b-0f5b21d3845f.png align="center")

* This will redirect you to the interface shown below. Here, you can run the instance within AWS Cloud itself and access it, or you can use the SSH Client to access this instance from your local machine, which is what we want.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539589729/85b67bc9-fed8-45df-9603-5ac2026b1283.png align="center")

* Before setting up SSH, remember that we downloaded the `Key-Pair`. Let's first place it in the correct location.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539669936/624e096c-440f-4ddd-8507-ddc669744599.png align="center")

* I am using a Mac, and I usually store my SSH keys inside the `.ssh` folder located in the home directory. Let's first navigate to the home directory.
    

```bash
cd ~/
```

* Now, move the key pair from the download folder to the .ssh folder using the `mv` command below:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539917008/9ca8ba85-d506-4bf8-8203-e4a364988814.png align="center")

* Once it’s done, we are good to go. So let’s follow these instructions.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762539953498/725997fd-ae22-49a8-bc4d-2a31daad1ee4.png align="center")

* Run `chmod` A command to change the permission to ensure your key is not publicly viewable.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762540006041/71c8f652-afd3-43cd-8b38-7a02ef3672d1.png align="center")

* Now run
    
* ```bash
    ssh -i "<your-key-name>.pem" ubuntu@<your-ip>
    ```
    
    to connect to the instance we created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762540063323/36c2dc8b-32e7-46f7-a3cc-f3f7a3cabf33.png align="center")

* Type `yes` and press Enter
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762540144370/f34169c9-4779-4188-af03-3e090fc2da09.png align="center")

* As you can see, we are now inside the instance we created. Isn't it cool that we can access it from our local machine?
    
* Now you can perform any tasks that you would normally do on your local machine.
    

---

# Installing/Updating Packages

* Now that we have our instance connected, before starting anything, we need to ensure we are using the latest packages in Ubuntu and install any available updates. To do this, we run two commands:
    

```bash
sudo apt update 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762569629578/dc523adf-19a2-483e-bf1f-907d6175a2b0.png align="center")

* Which refreshes package lists (checks for updates) and then
    

```bash
sudo apt upgrade
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762569742182/8fb1e954-8458-4f56-a118-dc81c726a5fe.png align="center")

* Which Installs available updates for installed packages
    

---

# Installing Node.js in an EC2 instance

* Now that we have all the latest packages, we need to install Node.js (or the backend framework/library you need).
    
* To do this, we need to download and run the NodeSource setup script, which configures the system to install Node.js version 20 from their official repository.
    
* Use the command below to do that:
    

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762569958288/abfe6fae-3158-4145-94fc-1e36dc2897c6.png align="center")

* Once the NodeSource repository is added, we need to install **Node.js** and **npm** (Node.js’s package manager) on our system to use Node.js.
    
* To do this, run the command below
    

```bash
sudo apt-get install -y nodejs
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762570037013/107a72fd-b2ee-43f0-abd2-9efd75fc4918.png align="center")

---

# Pushing Local App to EC2

* Now that we have the Node environment set up, we can upload our local Node.js app to this instance. We can do this using the SSH connection we already set up.
    

```bash
rsync -avz --exclude 'node_modules' --exclude '.git' --exclude '.env' \
  -e "ssh -i ~/.ssh/your-key.pem" \
  . ubuntu@ip-address:~/app
```

* In simple terms, this command copies the current folder (`.`) to the remote server’s `~/app` directory using SSH. It skips unnecessary files like `node_modules`, `.git`, and `.env` because we don't need those.
    

> NOTE: Be sure to replace ‘your-key’ with your SSH key name in the command above, and replace ‘ip-address’ with your actual IP address.

* To execute this command, go to your code directory and run the command above.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762570682270/4981a055-758d-4652-b6ca-e7bbe66ee73a.png align="center")

* If you now run the `ls` command in your instance's home directory, you will see the `app` folder has been created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762570770769/d4ca1d29-2c81-4c8d-a98b-37ee11e59e7e.png align="center")
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762570840301/a9b579be-75a0-41eb-b976-2a61a548d372.png align="center")
    
    And if you use `cd` to enter it, you will see all your source code.
    

---

# Setting up Environment (`.env`) File.

* If you have a database running locally, like PostgreSQL or MySQL, you can install those on this instance just like we did for Node.js.
    
* I have MongoDB running on MongoDB Atlas. So, to allow this instance to access the database, we need to add the instance's IP to the whitelist. Simply copy the instance's IP address and paste it into the IP Access List entry.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762571242267/e0e541c6-c091-40e3-a94e-459a4334adc9.png align="center")

* Now that everything is set up, we need one more file: the `.env` file. Remember, we excluded it when we transferred our files to the instance.
    
* So let’s create the `.env`file
    

```bash
cd app/
sudo vim .env # This will create and open .env file
```

```bash
# .env
# paste your environment variables
```

* You can exit the Vim editor by pressing `esc`, then `:` (colon), typing `wq`, and pressing enter.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624002875/5bb70b47-77b9-4978-9ba5-1d88b454ef93.png align="center")

* As you can see, we now have the `.env` file in place.
    
* Before we run our app, let’s make sure we have downloaded all the required packages by running
    

```bash
npm i
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624116285/70e3e5ff-cac7-41db-8837-75bd1fde59f3.png align="center")

* Now, if we run the app, it should run without any errors.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624131648/d43df60e-3c0a-40d0-9887-929ae89f9e7c.png align="center")

---

# Configuring Security Rules

* To check if it is running, go to the instance dashboard, select your instance, copy the Public IP address, and paste it into your browser.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624225373/a7974e5f-3fde-40a3-b4e2-5567b391460e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624308356/6a25bfde-598a-4a4b-b5fa-1976d5e5c599.png align="center")

* We can't see anything, and it didn't work. Why? Do you remember the security group we set up earlier?
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762624373812/a9d5be7e-a9dd-4d84-8647-ecbe891a9121.png align="center")

* We haven't specified our IP address and because we are accessing it from our machine we must add our IP address with port numner. So, let's add our IP address and the port number to the inbound rules and see if it works now.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762630234179/0d0385a9-a5c1-489f-a153-c878f8e1f6d2.png align="center")

* Click on Add Rules and add Custom TCP and specify your IP by selecting My IP.
    
* Now, if you run it, it should work fine. I am hitting `/test` the endpoint, which shows Hello World text.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762630310591/96b2183e-56d3-4bbf-aa2f-7a4c83195f5c.png align="center")

---

# Running App in Background (`systemd`)

* But here we have two major problems, and I hope you already know what they are.
    
* One big issue is that it's running on PORT `7575` and doesn't have a domain name. The second issue is that it's running on our local terminal, so if we close this terminal, we won't be able to access our server using that public IP address.
    
* First, let's address the second issue. To fix that, we need to find a way to run the application in the background so that no matter what we do in the terminal, the server will stay up the whole time.
    
* If you want to run your Node app as a background service, we use the `systemd` command.
    
* We need to create a service file. This file tells **systemd** (Linux’s init system) how to start, monitor, and restart your Node.js app as a background service, similar to how SSH or MongoDB are managed.
    
* Run the command below to create a new service file.
    

```bash
sudo vim /etc/systemd/system/myapp.service
```

* And paste lines below in it once Vim is opened
    

```bash
[Unit]
Description=Node.js App 
After=network.target multi-user.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/app
ExecStart=/usr/bin/npm start
Restart=always
Environment=NODE_ENV=production
EnvironmentFile=/home/ubuntu/app/.env
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=myapp

[Install]
WantedBy=multi-user.target
```

* In the \[Unit\] section, we include our app description and ensure our app starts *after networking* is ready (so Node can bind to a port).
    
* In the \[Service\] section, we specify how the app will run by including the working directory, environment, and other settings.
    

Now run

```bash
sudo systemctl daemon-reload
```

* Which Reloads systemd so it notices the new service file.
    

```bash
sudo systemctl enable myapp.service
```

* Enables the service to auto-start on boot.
    

```bash
sudo systemctl start myapp.service
```

* Start it right now (without reboot).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762631451599/094fcd1c-e82a-4831-ba3b-54c0b20efd6b.png align="center")

```bash
sudo systemctl status myapp.service
```

* Shows current status, logs, and whether it’s running or failed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762631568531/b15e0f4d-71d1-4fde-b10b-3da884193aa2.png align="center")

* And now, if you kill your terminal/app and still hit the URL, it should work.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762632046949/e294a052-e688-4423-8e1b-ceb4836c0dc0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762632115976/938cbc5e-eb78-493d-aa15-33ed98f00fc9.png align="center")

---

# Setting up Reverse Proxy (using Caddy)

* The next step is to allow HTTP access directly, without using PORT 7575. Then, we will add a domain name and an SSL certificate.
    
* To keep your actual web server, `localhost:7575`, hidden from the world and exposing only the HTTP and HTTPS ports, which are 80 and 443, we use reverse proxies like Nginx or Caddy.
    
* A **reverse proxy** is a server that sits **in front of your application servers** and manages all incoming client requests before sending them to your backend app, such as your Node.js service.
    
* We use this for security purposes. It allows us to add a firewall before requests reach the actual server. It also enables load balancing, as the reverse proxy can distribute requests to multiple servers.
    

```bash
http://54.86.58.33:7575/
```

We do

```bash
https://api.mydomain.com
```

* To implement this, there are many services like Nginx and Caddy. For this example, we'll use Caddy because it's easy to set up.
    
* Caddy is a **modern, lightweight reverse proxy and web server**, similar to Nginx but with a major advantage:
    
* Visit this [URL](https://caddyserver.com/docs/install#debian-ubuntu-raspbian) and run all the commands.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762632733100/756fe7e1-ae28-4565-8e35-e5c4ed799d46.png align="center")

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
chmod o+r /usr/share/keyrings/caddy-stable-archive-keyring.gpg
chmod o+r /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

* Once it is done, let’s remove the custom TCP rule we added in the security group for our IP
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762632841866/a2ecc0bc-249a-4834-96d0-f3c9edf75d34.png align="center")

* And now, if we run
    

```bash
sudo systemctl start caddy
```

* And then visit the IP address `54.86.58.33` Without mentioning any port, you should see a Caddy page
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762632983642/a5317fd6-d88b-4856-ab39-3ad2c5a87fe9.png align="center")

* But what we want is to forward the traffic to our application instead of showing this page. So, we will edit the Caddy file by opening it using the command below:
    

```bash
sudo vim /etc/caddy/Caddyfile
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762633152753/82190f95-4e98-4934-a962-ba5a69e806fe.png align="center")

* Comment down the `root` and `file_server` line and uncomment the `reverse_proxy` line and add your port.
    
* And now let’s restart Caddy
    

```bash
sudo systemctl restart caddy
```

* If you again run this URL, you should be able to see your app.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762634080934/e7f74781-5cb3-4a71-b50b-a3d3646c4a16.png align="center")

* That’s it, now you can use this URL anywhere to access the backend APIs.
    
* You can also set up a custom domain name and attach it to this current IP address (for example, example.com) or something like this using the Route53 service.
    

---

# Conclusion

* Thank you for taking the time to read my blog. I hope you enjoyed it and learned something new. I'll be sharing more about AWS soon as I continue to learn. Keep learning!!
    
* Until then…
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711803084752/aa266313-a315-41a8-9538-8ff4370577fb.gif?auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm align="center")

* Connect with me on [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/)**,** [**Github**](https://github.com/red-star25)**, and** [**Twitter**](https://twitter.com/dhruv_nakum)**.**