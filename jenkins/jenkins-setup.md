


```bash 
  docker run -d \
    --name jenkins \
    -p 8080:8080 \
    -p 50000:50000 \
    -v jenkins_home:/var/jenkins_home \
    -v /var/run/docker.sock:/var/run/docker.sock \
    jenkins/jenkins:lts

  sudo vim /etc/docker/daemon.json

  {
    "dns": ["8.8.8.8", "8.8.4.4"]
  }

  sudo systemctl restart docker
  docker restart jenkins
```

