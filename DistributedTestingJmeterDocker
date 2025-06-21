
# 🧪 Distributed Testing – By JMeter And Docker

## 📌 Introduction

In today's digital revolution, more and more services are being virtualized, and **Docker** is a key enabler of this shift.

Docker is an open-source platform that simplifies and optimizes the software lifecycle. It offers lightweight virtualization by sharing the host Linux kernel instead of emulating an entire operating system like traditional virtual machines.

### ⚖️ Docker vs Virtual Machines

| Feature         | Virtual Machine | Docker Container |
|----------------|------------------|------------------|
| OS Overhead     | High             | Low              |
| Performance     | Slower           | Faster           |
| Boot Time       | Minutes          | Seconds          |
| Isolation Level | Strong           | Moderate         |

---

## 🧱 Docker Basics Recap

Docker works in **two main phases**:

1. **Image Build Phase**  
   Define a minimal set of environment specifications (e.g., base Linux image, JMeter version).  
   ✅ Output: Docker **Image**

2. **Run Phase**  
   Launch containers from the image to run applications or test logic.  
   ✅ Output: Docker **Container**

---

## 📊 What is JMeter Distributed Testing?

**Distributed testing** splits one test across multiple machines to simulate heavy load or parallel users.

### 🔄 Client-Server Architecture

- **Client (Master)**: Loads `.jmx` script and orchestrates the test execution.
- **Servers (Slaves)**: Receive test plan and generate load on the target.

Using Docker, replicating and managing multiple slave environments becomes fast and consistent.

---

## 🛠️ Step-by-Step Setup Using Docker

### ✅ Pre-requisites

- Docker installed on your system (Windows, Linux, or macOS).
- Optional: Git Bash or WSL for better shell support on Windows.

---

### 🔹 Step 1: Pull or Build Docker Images

You can either build your own or use pre-built images:

#### 🛠️ Build Locally
```bash
cd /path/to/Dockerfile
docker build -t jmbase .
````

#### 🗂️ Or Pull Pre-Built Images from Docker Hub

```bash
docker pull mnazim1541/jmbase
docker pull mnazim1541/jmmaster
docker pull mnazim1541/jmslave
```

---

### 🔹 Step 2: Create Containers

#### 🎯 Master Container

```bash
docker run -dit --name master mnazim1541/jmmaster /bin/bash
```

#### 🧱 Slave Containers (Repeat to scale)

```bash
docker run -dit --name slave01 mnazim1541/jmslave /bin/bash
docker run -dit --name slave02 mnazim1541/jmslave /bin/bash
docker run -dit --name slave03 mnazim1541/jmslave /bin/bash
```

---

### 🔹 Step 3: Get IPs of All Containers

Use the following command to fetch IP addresses:

```bash
docker inspect --format '{{ .Name }} => {{ .NetworkSettings.IPAddress }}' $(docker ps -a -q)
```

---

### 🔹 Step 4: Access the Master Container

```bash
docker exec -it master /bin/bash
```

---

### 🔹 Step 5: Copy Scripts into the Master Container

#### 📄 Copy JMeter Test Plan

```bash
docker exec -i master sh -c 'cat > /JMeterFiles/JmeterDemo_Test_Script.jmx' < C:/DockerizedJMeter/JMeterFiles/JmeterDemo_Test_Script.jmx
```

#### ⚙️ (Optional) Replace `user.properties`

```bash
docker exec -i master sh -c 'cat > /jmeter/apache-jmeter-3.3/bin/user.properties' < C:/DockerizedJMeter/user.properties
```

---

### 🔹 Step 6: Run JMeter Tests

#### ▶️ Non-Distributed (Local in Master)

```bash
jmeter -n -t JmeterDemo_Test_Script.jmx -l Result.jtl
```

#### 🌐 Distributed Mode (Using Slave IPs)

```bash
jmeter -n -t JmeterDemo_Test_Script.jmx -R 172.17.0.3,172.17.0.4,172.17.0.5 -l Test_Result.jtl
```

---

### 🔹 Step 7: Retrieve Results

```bash
docker cp master:/JMeterFiles/Test_Result.jtl .
```

---

### 🔹 Step 8: Generate JMeter HTML Report

Ensure the target folder is empty:

```bash
jmeter -g Test_Result.jtl -o JMeterReport
```

---

## 📚 References

* [JMeter Distributed Testing Guide](https://jmeter.apache.org/usermanual/jmeter_distributed_testing_step_by_step.html)
* [Docker Official Docs](https://docs.docker.com/get-started/)
* https://qanovation.com/distributed-testing-jmeter-docker/
* [Blazemeter: JMeter + Docker](https://www.blazemeter.com/blog/jmeter-distributed-testing-with-docker)

```

