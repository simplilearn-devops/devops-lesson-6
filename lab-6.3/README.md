# Exercise 6.3 Using Git

In this exercise we will install a Git server in a Docker container
and use Git commands.

### Step 1

Connect to the Google Compute Engine virtual machine.

### Step 2

Change to the exercise directory. 
`cd`  
`cd devops-lesson-6/lab-6.3`  

Copy the SSH keys.  
`cp ~/.ssh/id_rsa.pub authorized_keys`  

Check out the Dockerfile.  
`cat Dockerfile`  

Build the Alpine Linux image.  
`docker build -t git .`  
`docker images`  

### Step 3

Run the container.  
`docker run -d -p 2022:22 --name git git`  
`docker ps`  

See that docker created a volume for the data.  
`docker volume ls`  
`docker inspect git`  

### Step 4

Clone the git repo.  
`git clone ssh://git@localhost:2022/home/git/project.git`  
`cd project`  
`ls -ls`  

Add a new file.  
`eco "message 1" > message1.txt`  
`git status`  
`git add *`  
`git status`  
`git commit -m "added message"`  
`git status`  
`git push`  
`git log message1.txt`  

Try some other Git commands.

### Step 5

Tidy up.  
`docker rm -f git`  
`rm -rf project`  

