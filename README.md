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
    ##workspace /var/jenkins_home/workspace/my-first-job
14) ## job-2: used this command in Jenkins command :
    ##On Jenkins shell:
        echo "current date and Time is: $(date)"
        echo "current user is: $(whoami)"
15) ## job-3: used this command in Jenkins command :
    ##On Jenkins shell:
    	NAME="Unni K"
        echo "Hello, $NAME. The current date and time is: $(date)"
16) ## job-4: used this command in Jenkins command :
    ##On Jenkins shell:
    	echo "Hello $NAME. The current date and time is: $(date)" > /tmp/info
    jenkins@8ce69885d87a:~$ cat /tmp/info
    jenkins@8ce69885d87a:~$ rm -f /tmp/info
    jenkins@8ce69885d87a:~$ cat /tmp/info
    --> run the job again
    jenkins@8ce69885d87a:~$ cat /tmp/info
    
18) Create a script in Local File system & copy to docker container
    ##Note: vi editor won't be available inside Docker container 
    vi script.sh
	#!/bin/bash
	NAME=$1
	LASTNAME=$2
	echo "Hello, $NAME $LASTNAME"
    chmod +x script.sh
    ./script.sh Unni KM
    
20) docker cp script.sh jenkins:/tmp/script.sh
    docker exec -it jenkins bash
    ls -l /tmp/script.sh
    cat /tmp/script.sh
    
22) ##From Jenkins:
    ##On Jenkins shell:
	/tmp/script.sh Unni KM
   ##OR
   ##On Jenkins shell:
	NAME1=Unni
	LASTNAME1=KM
	/tmp/script.sh $NAME1 $LASTNAME1

23) ##Add basic logic & Boolean parameters
    vi /tmp/script.sh
	#!/bin/bash
	NAME=$1
	LASTNAME=$2
	SHOW=$3
	
	if [ "$SHOW" = "true" ]; then
	    echo "Hello, $NAME $LASTNAME"
	else
	    echo "If you want to see the Name, Please mark the SHOW option"
	fi

    $ ./tmp/script.sh
	If you want to see the Name, Please mark the SHOW option

    $ ./tmp/script.sh Unni KM
	If you want to see the Name, Please mark the SHOW option

    $ ./tmp/script.sh Unni KM false
	If you want to see the Name, Please mark the SHOW option

    $ ./tmp/script.sh Unni KM true
	Hello, Unni KM
    	
24) ##Above script Running through Jenkins
--------------------------------------------------------------------------------------------
	Jenkins parameters:
--------------------------------------------------------------------------------------------
	FIRST_NAME
	Unni ---> Default value
	
	LASTNAME
	choices:
	Tom
	Myliatt
	Smith
	Doe
	
	Boolean Parameter
	SHOW
	Set by Default --> this checkbox make the value `true` by default

	##command shell:
	/tmp/script.sh $FIRST_NAME $LASTNAME $SHOW
------------------------------------------------------------------------------------------------
	Console Output
	Started by user Jenkins Admin
	Running as SYSTEM
	Building in workspace /var/jenkins_home/workspace/my-first-job
	[my-first-job] $ /bin/sh -xe /tmp/jenkins12555385524419567693.sh
	+ /tmp/script.sh Unni Myliatt true
	Hello, Unni Myliatt
	Finished: SUCCESS
------------------------------------------------------------------------------------------------
	Console Output
	Started by user Jenkins Admin
	Running as SYSTEM
	Building in workspace /var/jenkins_home/workspace/my-first-job
	[my-first-job] $ /bin/sh -xe /tmp/jenkins8328500223048601920.sh
	+ /tmp/script.sh Unni Doe false
	If you want to see the Name, Please mark the SHOW option
	Finished: SUCCESS
 ------------------------------------------------------------------------------------------------
