# DevOps Intro
## Life before DevOps
### Why DevOps
#### Key Pillars of DevOps
##### Monolith Architecture 


### Development Environment 
![](images/dev-env.png)
- **DevOps Introdction**
- DevOps is a culture that bridges the gap between Development and Operation

- **Life before DevOps**
- Waterfall - V-Model
- Transition to Agile and SCRUM

- Create `vagrantfile` in the current location
```
Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"
# creating a virtual machine ubuntu 


# assign private ip to our VM
 config.vm.network "private_network", ip: "192.168.10.100"   

 # Ensure to install hostsupdater plugin on our localhost before rerunning the vagrant
 config.hostsupdater.aliases = ["development.local"]

 # Sync folder from OS to VM
 config.vm.synced_folder ".", "/home/vagrant/app"
 
end

```
- create `provision.sh`
```
#!/bin/bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y

```
- Vagrant commands:
```
Common commands:
     autocomplete    manages autocomplete installation on host
     box             manages boxes: installation, removal, etc.
     cloud           manages everything related to Vagrant Cloud
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     hostsupdater
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination   
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     upload          upload to machine via communicator
     validate        validates the Vagrantfile
     version         prints current and latest Vagrant version
     winrm           executes commands on a machine via WinRM
     winrm-config    outputs WinRM configuration to connect to the machine
```

### Linux commands
- Who am I `uname` or `uname -a`
- Where am I `pwd` will display current location
- How can I list contents including hidden files `ls -a`
- Delete file `rm filename` or `rm -rf filename`
- Create a file `touch filename` or `nano filename`
- create a dir `mkdir dir_name`
- navigate inside dir `cd name_dir
- List all processes running `ps aux` or `top`
- How to kill a process `kill process id/s`
- wild card is used to deal with multiple files with same extention `*`
- file permissions `+x executable`  
- `read (r) write (w)`
- check permissions `ll`
- change permision `chmod permision_required filename`
- `tail `
- Copy file or folder command in linux?
- `cp file_path_you_want_2_copy destination_to_copy_the_to`
- cut paste - move fil or folder `mv`
- How to use piping | `ls | head -2`

-**Variable and Environment Variable**
- How to check env var? `env`
- Creating env var `export key=value` 
- `export name=shahrukh`
- `printenv name`
- `export DB_HOST="mongodb://192.168.10.150:27017/posts"`



### Reverse Proxy with Nginx
![](images/Screenshot%20(152).png)
```

server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
- create a file for nginx.conf on localhost
  ```
  server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

```
 
- create a file for mongod.conf
```
net:
  port: 27017
  bindIp: 0.0.0.0
```

- provision.sh for app
```
# set up an env var once the db is up
# seeds db if needed
```
- provision.sh for db
```

```
- 
- 
- add dependencies in .gitignore
- restart app and db once conf is changed








