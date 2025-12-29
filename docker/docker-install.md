# **Docker Install**

### 🧩 Step 1: System Update
```
sudo apt update && sudo apt upgrade -y
```
### 🧩 Step 2: Docker Install

```
sudo apt install -y docker.io
```

### 🧩 Step 3: Docker start + enable and version check

```
sudo systemctl start docker
sudo systemctl enable docker

sudo usermod -aG docker $USER
docker --version
```
