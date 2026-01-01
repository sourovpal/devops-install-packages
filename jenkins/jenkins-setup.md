# Jenkins Install In Docker

### 🧩 Step 1: Pull Jenkins Image with Run

```bash
  # Pull Only Image
  docker pull jenkins/jenkins:lts

  # Pull Image With Run 
  docker run -d \
    --name jenkins \
    -p 8080:8080 \
    -p 50000:50000 \
    -v jenkins_home:/var/jenkins_home \
    -v /var/run/docker.sock:/var/run/docker.sock \
    jenkins/jenkins:lts

  # Get initial Admin Password
  docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

  # Offline
  # This Jenkins instance appears to be offline.
  sudo vim /etc/docker/daemon.json
  { "dns": ["8.8.8.8", "8.8.4.4"] }

  # Restart Docker and Jenkins Container
  sudo systemctl restart docker
  docker restart jenkins
```

### 🧩 Open Jenkins Container Terminal
```bash
docker exec -it jenkins bash             # bash or sh
```

# Jenkins Install With Connect Host Machine Docker

### 🧩 Step 1: Rewrite Dockerfile for Jenkins
```bash 
  FROM jenkins/jenkins:lts
  
  USER root
  
  # Install Docker CLI only (no daemon)
  RUN apt-get update && \
      apt-get install -y docker.io && \
      rm -rf /var/lib/apt/lists/*
  
  # Add jenkins user to docker group
  RUN usermod -aG docker jenkins
  
  USER jenkins
```

### 🧩 Step 2: Rebuild Jenkins Image
```bash
  docker build -t jenkins-with-docker .
```

### 🧩 Step 3: Run Image in Container
```bash
  docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v jenkins_home:/var/jenkins_home \
  jenkins-with-docker
```

# Build Custom Jenkins Image with SSH For Production

### 🧩 Step 1: Build Jenkins Image Dockerfile
Dockerfile

```bash 
  FROM jenkins/jenkins:lts
  
  USER root
  
  RUN apt-get update && \
      apt-get install -y openssh-client && \
      rm -rf /var/lib/apt/lists/*
  
  RUN mkdir -p /var/jenkins_home/.ssh && \
      chmod 700 /var/jenkins_home/.ssh
  
  COPY id_rsa /var/jenkins_home/.ssh/id_rsa

  RUN chmod 600 /var/jenkins_home/.ssh/id_rsa

  RUN apt-get update && apt-get install -y && \
    git && \
    docker.io && \
    curl
  
  RUN chown -R jenkins:jenkins /var/jenkins_home/.ssh
  
  USER jenkins
```



