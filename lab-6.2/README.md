# Exercise 7.3 Configuration Management with Puppet

We will now pull and run a puppet server and a puppet client in
Docker containers.

### Step 1

Create a Docker network for puppet.

`docker network create puppet`  

Check what got created.

`docker network ls`  

### Step 2

Pull the puppet images.

`docker pull puppet/puppetserver-standalone`  
`docker pull puppet/puppet-agent-alpine`  
`docker images`  

### Step 3

Start the puppet server.

`docker run --net puppet -d --name puppetserver --hostname puppet puppet/puppetserver-standalone`  
`docker ps`  

We need to ensure that the server is running. Extract the logs until you see
the message:  
Puppet Server has successfully started and is now ready to handle requests  
`docker logs puppetserver`  

### Step 4

Start the puppet agent. It will connect to the server and perform a certificate exchange. Check out the output.

`docker run --rm --net puppet --link=puppetserver:puppet puppet/puppet-agent-alpine`  

### Step 5

Now let's find out what package puppet is managing.

`docker run --rm --net puppet --link=puppetserver:puppet puppet/puppet-agent-alpine resource package`  

### Step 6

Tidy up.

`docker rm -f puppetserver`  

