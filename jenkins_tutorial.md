Jenkins Tutorial

## Install through docker
Prompt PowerShell:
```
docker run -u root --rm -d -p 8080:8080 -p 50000:50000 -v jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkinsci/blueocean
```

Get container id:
```
docker container ls
```
to get id of jenkins container, then to get temporary password and run:
```
docker exec f651e444fd9c   cat /var/jenkins_home/secrets/initialAdminPassword
```

Access the jenkins
```
docker exec -it container_id bash
```
