# Exercise 6.3 Using Git

In this exercise we will install a Git server in a Docker container
and use Git commands.

### Step 1

Connect to the Google Compute Engine virtual machine.

### Step 2

Change to the exercise directory and ensure it is up to date.  
`cd`  
`cd devops-lesson-6`  
`git pull`  
`cd lab-6.3`  

Copy the SSH keys and clean the known hosts file.    
`cp ~/.ssh/id_rsa.pub authorized_keys`  
`rm -f ~/.ssh/known_hosts`  

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

Clone the git repo. Ignore the warning about the repo being empty. It is.  
`git clone ssh://git@localhost:2022/home/git/project.git`  
`cd project`  
`ls -la`  

Add a new file. See how the status changes.  
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
`docker mi git`  
`rm -rf project ~/.ssh/known_hosts`  

