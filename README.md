# docker-repo

1) curl:
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2) sudo chmod +x /usr/local/bin/docker-compose
3) docker pull jenkins/jenkins
4) docker images
5) docker ps
6) docker ps -a   --> shows the container with exit status.
7) Location where the docker files will be stored:
   $ docker info | grep -i root
      Docker Root Dir: /var/lib/docker
   $ sudo du -sh /var/lib/docker
      3.8G    /var/lib/docker
8) Note:--once jenkins docker container is created, the id of the jenkins user inside it will be 1000
      #Change file/directories ownership recursively in Linux
      $ sudo chown 1000:1000 jenkins_home -R
9) docker logs -f <container-name>
      docker logs -f jenkins
10)
    ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
		Setup Local DNS For Jenkins:
    ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
      1)Right click on a notepad & Run as Administrator 
      2) Open below file
      C:\Windows\System32\drivers\etc\hosts
      
      3)
      Add VM-IP: like below in hosts file & save
      192.168.56.3 jenkins.local
      
      4) Open browser using below link:
      http://jenkins.local:8080
      user name: admin
      pwd: 1234
   ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

11) docker exec -it jenkins bash
12) job-1: Create a New Job: my-first-job
    -------------------------------------
	Dashboard-->New Item -->Enter an item name-->my-first-job-->Freestyle project-->OK-->Build-->Add Build Step-->Execute Shell-->
        Command--->
	echo Hello World
	--> Save--Build Now-->Build History-->Console Output
    ## workspace /var/jenkins_home/workspace/my-first-job
14) ## job-2: used this command in Jenkins command :
    ## On Jenkins shell:
        echo "current date and Time is: $(date)"
        echo "current user is: $(whoami)"
15) ## job-3: used this command in Jenkins command :
    ## On Jenkins shell:
    	NAME="Unni K"
        echo "Hello, $NAME. The current date and time is: $(date)"
16) ## job-4: used this command in Jenkins command :
    ## On Jenkins shell:
    	echo "Hello $NAME. The current date and time is: $(date)" > /tmp/info
    jenkins@8ce69885d87a:~$ cat /tmp/info
    jenkins@8ce69885d87a:~$ rm -f /tmp/info
    jenkins@8ce69885d87a:~$ cat /tmp/info
    --> run the job again
    jenkins@8ce69885d87a:~$ cat /tmp/info
18) 
    	
