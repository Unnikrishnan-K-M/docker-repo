# docker-repo

1) curl:
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2) sudo chmod +x /usr/local/bin/docker-compose
3) docker pull jenkins/jenkins
4) docker images
5) Location where the docker files will be stored:
   $ docker info | grep -i root
      Docker Root Dir: /var/lib/docker
