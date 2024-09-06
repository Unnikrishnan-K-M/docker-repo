# docker-repo

1) curl:
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2) sudo chmod +x /usr/local/bin/docker-compose
3) docker pull jenkins/jenkins
4) docker images
5) Location where the docker files will be stored:
   $ docker info | grep -i root
      Docker Root Dir: /var/lib/docker
   $ sudo du -sh /var/lib/docker
      3.8G    /var/lib/docker
7) Note:--once jenkins docker container is created, the id of the jenkins user inside it will be 1000
      #Change file/directories ownership recursively in Linux
      $ sudo chown 1000:1000 jenkins_home -R
8) docker logs -f <container-name>
      docker logs -f jenkins
9) ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
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
