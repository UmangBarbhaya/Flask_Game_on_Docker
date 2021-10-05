# Virtualization and Cloud computing
---
### Assessment 1: Virtual Machines and Dockers
#### Part 2: Docker Application Deployment
---
##### Author:
Umang Barbhaya\
M20CS017

##### Course Instructor: 
Dr. Sumit Kalra \
Assistant Professor\
Department of Computer Science & Engineering\
Indian Institute of Technology, Jodhpur\

---
#### Process Followed:
Below is the process that I followed to create this Application
- I Installed Windows Subsystem for Linux using following command
 ```sh
wsl --install
```
- Then Enabled the Virtualization support from BIOS settings
- Downloaded and installed docker using the steps from https://docs.docker.com/desktop/windows/install/
- After installation of Docker Destop I registered to docker hub and signed in to docker hub via Docker Desktop
- Created a Folder and inside that created a Dockerfile with following content.
```sh
FROM ubuntu:20.04
RUN apt update && apt -y upgrade
RUN apt install -y python3-pip
RUN apt install -y python3-venv
RUN pip3 install flask
EXPOSE 5001
```
I have selected Ubuntu version 20.04 as my base images. Pulled that image from docker
After that updated and upgraded the ubuntu packages. Ubuntu:20,04 comes by default loaded with Python3. Post that installed pip3, venv packages for python and then installed flask using pip3.
Once this is done Exposed the port 5001 for running the flask application.
- Created a new repository in docker hub (https://hub.docker.com/) as umangbarbhaya/ubuntuflask
- After Dockerfile creation we build the docker image with above configuration using below command and gave its version as v1
``` sh
docker build . -t ubuntuflask
docker image build -t umangbarbhaya/ubuntuflask:v1 .
```
- After creating the docker image verified the image by searching using below command
``` sh
docker images
```
- Pushed the docker image to the the docker hub repository as below
``` sh
docker image push umangbarbhaya/ubuntuflask:v1
```
###### After the image is pushed we need to use this image to run our flask based web application
- Created a new folder and stored the Flask based web application in this folder
- Also created a new Dockerfile with following content
``` sh
FROM umangbarbhaya/ubuntuflask:v1
COPY . /app
WORKDIR /app
RUN python3 -m venv venv
RUN /bin/bash -c "source venv/bin/activate"
ENTRYPOINT [ "python3" ]
CMD [ "main.py" ]
```

Here are the details of above file: Download the image of Ubuntu along with Flask microsevices that we had created and pushed earlier. The next line signifies to copy the content of current host machine folder to the /app location in the Ubuntu OS. After that create /app as the working directory. After that create a virtual environment in that folder using venv and execute the python file main.py. Note: The last line signifies the name of file which is main.py in my case.
- Build the image of the above file using 
```sh
docker build . -t shinchangame
```
- Now our Web application image is created and we have to create a container and run the container for this image. Below is the command for that
```sh
docker run --name shinchangame -p 5001:5001 shinchangame
```
We are giving the container name as "shinchangame" and keeping both host machine and container port as 5001 and then running the image "shinchangame" that we had created

![image](https://user-images.githubusercontent.com/82836595/131711254-91d60274-ed5d-49dd-8c53-9df4ab2b55a2.png)
- As seen in above image our application as executed and you can access the application via link ```http://localhost:5001/```
- Below is the screen shot of how our shinchangame looks like
![image](https://user-images.githubusercontent.com/82836595/131712026-9164893b-4885-405a-b5dd-86c15723650a.png)

#### Application Functionality

 I have created an image consisting of Ubuntu:20.04 and Python's Flask which is a micro web framework to execute the Flask based web applications. After creating this image we have pushed this image to docker hub.
After this I have created a Game. The game is to find the extra image on the left side. This game is being created using basic web development tools like HTML, CSS and Javascript and flask microframework.
This Web application is then executed on the docker image that we had pushed on the docker hub.

#### Github Repository details
This is the link for the github repository: https://github.com/UmangBarbhaya-IITJ/M20CS017
We have uploaded both the Dockerfile and the Flask based game application onto this repository.
###### Unit Details
- In the Repository M20CS017 there are two folders /ubuntuflask /shinchangame.
- The folder /ubuntuflask contains the Dockerfile which creates the image umangbarbhaya/ubuntuflask:v1. This new image is created by taking ubuntu:20.04 as base image and installing python dependencies and flask.
- The folder /shinchangame contains the Dockerfile which creates the image of our game. 
- Also the /shinchangame contains main.py which is our Python Flask application file which will be executed to run the game
- /shinchangame folder has two more folders /static and /templates
- /templates folder contains our html file index.html 
- /static folder contains 3 more folders /css /js /images to store css, Javascript and image files respectively

#### Execute Web Game in your Windows 10 machine
- Install docker from https://docs.docker.com/desktop/windows/install/
- Login to your dockerhub account. If you don't have an account you need to first create it
- Clone the repository M20CS017
- Open CMD and go to the folder <Your path>\M20CS017\shinchangame\
- Type the below command in CMD to build the image. In place of shinchangame you can give any name.
```sh
docker build . -t shinchangame
```
- Type the below command to create container and run the application. Note: give the same name that you had given above
```sh
docker run -p 5001:5001 shinchangame
```
- Access the game using below link
```http://localhost:5001/```
