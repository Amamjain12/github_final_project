

Part A – Configure Git
Open Git Bash.
Set global username:
Command : git config --global user.name "your username"
Output : Set global email:
Command : git config --global user.email "your email id"
Output : 

Part B – Create Local Repository and Files
Go to the home folder (optional, if not already there):
Command :  cd ~
Create and open project folder:
Command : mkdir folder name & then cd folder name
Output : 

Initialize Git repository:
Command : git init
Output : 

Create three files:
Command : touch file_name
Output : 

Open and edit the files using Notepad:
Command : notepad file_name
Output : 

Part C – Stage and Commit Files
Check current status:
Command : git status
Output : 
Add all files to staging area:
Command : git add .
Output : 
Commit the files:
Command : git commit -m "Message to display"
Output : 

Part D – Create & Connect GitHub Repository
Steps : Login to GitHub → click New repository → create a repository named DevOps-Lab-1 (without README).

Back in Git Bash, add remote origin:
Command : git remote add origin “repository path”
Output : 
Push the code to GitHub:
Command : git push -u origin master
Output : 


Part E – Basic Commands: status, log, pull
Check repository status:
Command : git status
Output : 
View commit history:
Command : git log
Output : 
Pull from remote (to check sync):
Command : git pull
Output : 

Part F – Clone Repository (from GitHub to Local)
Go one level up from current folder:
Command : cd ..
Output : 
Clone the same repository from GitHub:
Command : git clone “repository link”
Output : 
Go inside cloned folder:
Command : cd folder_name
Output : 

Part G – Branching and Merging
Create and switch to a new branch:
Command : git checkout -b new-branch
Output : 

Edit any file and add one new line using:
Command : notepad file_name
Output :
Stage and commit the change:
Command : git add .
git commit -m "Updated notes from new-branch"
Output : 
Switch back to master branch:
Command : git checkout master
Output : 
Merge the new branch into master:
Command : git merge new-branch
Output : 
Push merged changes to GitHub:
Command : git push
Output : 

Diagram/Architecture:-

Conclusion:-
This practical provided hands-on experience with Git and GitHub, covering the complete workflow from repository initialization to branching, merging, and remote collaboration. Mastery of these tools is fundamental to DevOps, as version control forms the foundation of any CI/CD pipeline.


















Practical : 3 : Jenkins CI Pipeline Using Blue Ocean
Aim:- 
To install and configure Jenkins on a Windows system, set up a CI/CD pipeline using the Blue Ocean interface, create multi-stage pipelines (Build, Test, Deploy), handle pipeline failures, and implement advanced pipeline features using Jenkinsfile with environment variables.

Theory:-
Jenkins is an open-source automation server written in Java that enables developers to build, test, and deploy software continuously, making it one of the most widely used CI/CD tools in DevOps. Blue Ocean is Jenkins' modern visual interface that provides a sophisticated pipeline visualization, making it easier to create, monitor, and debug pipelines through a graphical editor. Key Jenkins concepts include Pipelines, Stages (Build, Test, Deploy), Steps, Agents, Jenkinsfiles, and build Artifacts — all of which together define a complete automated delivery workflow. Jenkins supports environment variables like BUILD_NUMBER and BRANCH_NAME, which can be accessed within a Jenkinsfile for dynamic pipeline behavior. The Jenkinsfile approach (Pipeline as Code) ensures CI/CD configuration is version-controlled alongside application code, enabling reproducibility and easier team collaboration.

Phase 1: Environment Setup
Step : Java Installation (JDK 17.0.12)
Java Installation (Version 17.0.12)
Begin by installing Java. You can download version 17.0.12 from the following link:
https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html

Step : Install Java JDK 17 (64-bit) by selecting the destination folder (default C:\Program Files\Java\jdk-17\ or change if required) and click Next to continue the installation.

Phase 2: Jenkins Installation & Initial Configuration
Step : Installation of Jenkins
Link to download : https://www.jenkins.io/

Step : Download Jenkins 2.528.3 LTS by selecting the Windows installer from the Jenkins official website.

Step : Choose the default installation path C:\Program Files\Jenkins\ and click Next.

Step : Select Run service as LocalSystem and click Next to continue installation.

Step : Enter port number 8080, click Test Port, and then click Next.

Step : Browse and select the installed JDK path (e.g., C:\Program Files\Java\jdk-17) and click Next.

Step : Verify the correct Java 17 path is selected and proceed by clicking Next.

Step : Keep default options (Start Service enabled) and click Next to continue installation.

Step : Click on the Install button to start installing Jenkins 2.528.3 on the system.

Unlock Jenkins & Plugin Installation
Step : Open Jenkins in a web browser using http://localhost:<selected_port> to start the initial configuration. (For example my port is 8080 so the link is http://localhost:8085)
Step : Copy the initial administrator password from C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword and paste it on the Unlock Jenkins page, then click Continue.

Step: Click on Install suggested plugins to automatically install the recommended Jenkins plugins and complete the initial setup.

Admin User & URL Configuration
Step : Create the Jenkins admin user by entering Username(admin), Password(admin123), Full Name, and Email Address, then submit to complete the account setup.

Step : Enter the Jenkins URL as http://localhost:8085/ and save the configuration.

Phase 3: Blue Ocean Setup
Step : Click the gear icon → Manage Jenkins. 
Step : Search for "Blue Ocean" in the Available Plugins section, accessible by clicking on "Plugins."

Step : Select the checkbox and proceed with the installation.

Step : Open Blue Ocean – Click the menu (☰) and select Open Blue Ocean to use the visual pipeline interface.

Phase 4: Pipeline Creation Using Blue Ocean
Step : Welcome to Jenkins – Click Create a new Pipeline to start creating your first pipeline.

Step : Select Git as the source code management option.
Step : Enter the local Git repository path and click Create Pipeline.

Step : Click Create Pipeline to manually define the pipeline steps.

Step : Choose Agent: any and proceed to add stages.

Build Stage Configuration
Step : Click + Add step under the Build stage.

Step : Select Windows Batch Script as the build step & Add script command – Enter echo "Compiling" in the Script box and save the pipeline



Step : Jenkins pipeline was executed successfully, code was checked out from Git repository, and build step completed without errors.
IMPORTANT NOTE:
In case an error occurs while executing the build stages, please follow the steps outlined below.
Step 1 : Press Windows + R
Step 2 : Type services.msc
Step 3 : Find Jenkins
Step 4 : Right-click → Stop
Step 5: Go to Search bar and search for Notepad
Step 6 : Right click Run →  as Administrator
Step 7 : In Notepad → Open File → Go to Jenkins Folder → Find file name jenkins.xml → click on it 
Step 8 : Find these line and change it to : 
Line to find : 
<arguments>-Xrs -Xmx256m -Dhudson.lifecycle=hudson.lifecycle.WindowsServiceLifecycle</arguments>
Change to : 
<arguments>-Xrs -Xmx256m -Dhudson.lifecycle=hudson.lifecycle.WindowsServiceLifecycle -Dhudson.plugins.git.GitSCM.ALLOW_LOCAL_CHECKOUT=true</arguments>
Step 9 : Save and Close Notepad
Step 10 : Now again press Windows + R and type services.msc
Step 11 : Find Jenkins → Right Click → Start
Step 12 : Now ReRun the Pipeline and see that your pipeline is working.

Step : Set up the Test Stage identically to the Build Stage, with the only modification being the script content.

Step :  The Test Stage was also successful. 

Step : Implement the Deploy Stage using the same procedure as the previous stages.

Step :  The Deploy Stage was also successful. 

Step : Implement the End Stage using the same procedure as the previous stages.

Step :  The Deploy Stage was also successful.

Step : Nested Stages inside Build
Step : Within the main Build Stage, introduce two sub-stages: the Build Stage and Archive the Artifacts. 

Step : The 'Archive the Artifacts' stage should be completed by following the steps demonstrated in the image provided below.

Step : The creation of all stages within the Build Stage was successful.

Phase 5: Handling Failures
Introduce a Failure
Step 1 : Modify app.py in Step 1 by including the line: print("This is a buggy version of the app").

Step 2 : Edit the Test stage in Blue Ocean.
Step 3 : Edit Batch Script: Set content to echo Running critical tests... && exit 1
Step 4 : Save and Run the pipeline
Result:
The Test stage failed due to exit code 1.
Jenkins stopped further stages.
The pipeline was marked as FAILED.
Output:

Phase 6: Environment Variables (Advanced Pipeline)
Step : Jenkinsfile Creation
Step : Created a Jenkinsfile in the project root.

Step : Added an Initialize stage before the Build stage.
Code:
pipeline {
    agent any

    stages {

        stage('Initialize') {
            steps {
                bat '''
                echo Building branch: %BRANCH_NAME%
                echo Build Number: %BUILD_NUMBER%
                '''
            }
        }

        stage('Build') {
            steps {
                bat 'echo "Compiling"'
                bat 'echo "Build Version 1.0" > build-info.txt'
                archiveArtifacts artifacts: 'build-info.txt', allowEmptyArchive: true
            }
        }

        stage('Test') {
            steps {
                bat 'echo "Tests Passed"'
            }	
        }

        stage('Deploy') {
            steps {
                bat 'echo "Deploying application"'
            }
        }

        stage('End') {
            steps {
                bat 'echo "Pipeline completed successfully"'
            }
        }
    }
}
Step : Printed Jenkins environment variables:
BRANCH_NAME
BUILD_NUMBER
Step : Git Operations
Step : Committed Jenkinsfile to Git repository.
Commands used : 
git status
git add file_name
git commit 
Step : Triggered pipeline execution from Jenkins.

Diagram/Architecture:


Conclusion:-
This practical demonstrated the complete setup of Jenkins as a CI/CD automation server, along with visual pipeline management using Blue Ocean. The Jenkinsfile (Pipeline as Code) approach ensures CI/CD configuration is version-controlled, reproducible, and prevents faulty code from reaching production.


Practical : 5 : Docker and Docker Compose
Title: Installation and Basic Setup of Docker on Windows
Aim:-
To install Docker Desktop on a Windows system, verify the installation by running a test container, create a custom Docker image using a Dockerfile, and understand the basic Docker workflow including building images, running containers, and using Docker Compose to orchestrate multi-container applications.

Theory:-
Docker is an open-source platform that automates application deployment inside lightweight, portable containers — standardized units that package code along with all its dependencies to ensure consistent execution across different environments. Its client-server architecture consists of the Docker client, Docker daemon, images, containers, Dockerfiles, Docker Hub, volumes, and networks, all working together to manage the complete container lifecycle. Unlike virtual machines, Docker containers share the host OS kernel, making them significantly more lightweight, faster to start, and more resource-efficient — often just a few MB compared to several GB for a full VM. Docker Compose extends this further by allowing developers to define and run multi-container applications using a single docker-compose.yml file and start the entire stack with one command. Together, Docker and Docker Compose solve the classic "it works on my machine" problem by providing consistent environments from development through to production.

Step 1: 
Download Docker Desktop : https://docs.docker.com/desktop/setup/install/windows-install/
Open the official Docker installation page.
Click on Docker Desktop for Windows – x86_64.
Download the installer file.

Step 2: Configure Installation Settings
Select the following options:
Use WSL 2 instead of Hyper-V (recommended)
Allow Windows Containers to be used with this installation
Add shortcut to desktop
Click OK.

Step 3: Complete Installation
Installation completed message will appear.
Click on Close and Restart.
Restart your system.

Step 4: Accept Subscription Agreement
Open Docker Desktop.
The subscription agreement screen will appear.
Click Accept.

Step 5: Sign In to Docker
Select Personal option.
Click Continue with Google.
Enter a valid username.
Complete sign-up process.



Step 6: Update WSL (Linux Subsystem)
Open Command Prompt as Administrator and type: wsl --update

Step 7: Verify Docker Installation
Run the following command: docker run hello-world
Expected Output:
Hello from Docker!
This message shows that your installation appears to be working correctly.

Step 8: Create a Dockerfile
Create a folder named docker-test and inside it create a file named Dockerfile.
Add:
FROM ubuntu
CMD echo Hello BCA Students


Step 9: Build Docker Image
Run: docker build -t helloimage 

Step 10: Run Docker Image
Run: docker run helloimage
Output:
Hello BCA Students


Practical : 6 : Docker Compose : Part B
Step 1 — Create Folder
Open Command Prompt:
mkdir compose-demo
cd compose-demo

Step 2 — Create docker-compose.yml
Run: notepad docker-compose.yml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
Step 3 — Run Docker Compose
Command: docker compose up -d

Step 4 — Verify
Run: docker ps

Open browser: http://localhost:8080

Step 5 — Stop
docker compose down
 

Diagram/Architecture:-
Part A : Docker

Part B : Docker Compose




Practical : 7 : Ansible
Aim:-
To install and configure Ansible on a Windows system using Windows Subsystem for Linux (WSL), create and execute an Ansible playbook for basic automation tasks, and understand the fundamental concepts of Infrastructure as Code (IaC) and configuration management using Ansible.

Theory:-
Ansible is an open-source IT automation tool developed by Red Hat that simplifies configuration management, application deployment, task automation, and multi-node orchestration without requiring any software installed on managed nodes — making it truly agentless. It communicates with remote machines over SSH (or WinRM for Windows) using YAML-based Playbooks, which define the tasks to execute on target hosts through reusable components called Modules, organized via an Inventory file. Ansible follows a push-based architecture where the control node pushes configuration changes to managed nodes, executes tasks defined in playbooks, and returns results — all without persistent agent processes running on the managed systems. Since Ansible doesn't run natively on Windows, Windows Subsystem for Linux (WSL) provides a Linux environment within Windows, enabling Ansible to function without a separate virtual machine. Its simple syntax, agentless design, and powerful automation capabilities make Ansible one of the most widely adopted tools for Infrastructure as Code in DevOps workflows.

Installation, Setup and Basic Automation using Ansible on Windows (WSL)
Step 1: Install WSL
Command - wsl --install

Step 2: Update Ubuntu
Command - sudo apt update


Step 3: Install Ansible
Command - sudo apt install ansible -y

Step 4: Verify Installation
Command - ansible --version

Step 5: Create Working Directory
Commands:
cd ~
mkdir ansible_lab
cd ansible_lab
Step 6: Create Playbook
Command - nano basic_playbook.yml
Playbook Content:
---
- name: Basic Ansible Automation
  hosts: localhost
  connection: local

  tasks:
    - name: Create a text file
      file:
        path: /home/ishika/ansible_file.txt
        state: touch

Step 7: Execute Playbook
Command : ansible-playbook basic_playbook.yml

Step 8: Verify File Creation
Commands:
ls /home/ishika
cat /home/ishika/ansible_file.txt


Diagram/Architecture:-


Conclusion:-
This practical introduced Ansible as a powerful agentless automation tool, demonstrating how YAML-based playbooks can automate configuration tasks across managed nodes. Its simplicity and agentless design make it one of the most accessible and widely adopted Infrastructure as Code tools in DevOps.



Practical : 9 : Kubernetes
PART A: Installation & Setup
Step 1: Install Docker Desktop
Download Docker Desktop
Install with default settings
Ensure Docker shows “Docker is running”
Step 2: Install kubectl (Steps are provided at the end)
Download kubectl.exe
Place inside C:\kubectl
Add folder to PATH
Verify: kubectl version --client

Step 3: Install Minikube (Steps are provided at the end)
Download Minikube installer
Install with default settings
Verify: minikube version


PART B: Start Kubernetes Cluster
Step 4: Start Minikube
In command prompt paste : minikube start --driver=docker

Step 5: Verify Cluster
In command prompt paste:
kubectl cluster-info
kubectl get nodes

PART C: Deploy Application
Step 6: Create Pod
Create pod.yaml
Apply:
kubectl apply -f pod.yaml
kubectl get pods
Paste these when you paste the command notepad pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80

Step 7: Create Deployment
Create deployment.yaml
Apply:
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
Paste these when you paste the command notepad deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80

Step 8: Create Service
Create service.yaml
Apply:
kubectl apply -f service.yaml
kubectl get services
Paste these when you paste the command notepad service.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007

Step 9: Access Application
Run: minikube service nginx-service


PART D: Scaling Application
Scale deployment:
kubectl scale deployment nginx-deployment --replicas=3
kubectl get pods


Installation and Setup of Kubernetes Tools (kubectl and Minikube)
Step 1: Open PowerShell as Administrator
Press Windows key
Type PowerShell
Right-click → Run as Administrator
Step 2: Create Folder for kubectl
Command: New-Item -Path "C:\" -Name "kubectl" -ItemType Directory -Force
Step 3: Download kubectl.exe
Command: Invoke-WebRequest -Uri "https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl.exe" -OutFile "C:\kubectl\kubectl.exe"
Step 4: Add kubectl to System PATH
Press Windows key
Search Environment Variables
Click Edit the system environment variables
Click Environment Variables
Under System Variables → Select Path
Click Edit → New
Add: C:\kubectl
Click OK → OK → OK
Step 5: Verify Installation
Close PowerShell and open a new Command Prompt.
Command: kubectl version --client

PART B: Install Minikube Using Command Line
Step 1: Open PowerShell as Administrator
Step 2: Create Folder for Minikube
Command: New-Item -Path "C:\" -Name "minikube" -ItemType Directory -Force

Step 3: Download Minikube
Command: Invoke-WebRequest -Uri "https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe" -OutFile "C:\minikube\minikube.exe"

Step 4: Add Minikube to PATH
Repeat the Environment Variables steps and add: C:\minikube

Step 5: Verify Minikube Installation
Open a new Command Prompt.
Command: minikube version
PART C: Start Kubernetes Cluster
Step 1: Start Cluster
Ensure Docker Desktop is running.
Command: minikube start --driver=docker

Step 2: Verify Cluster
Command:
kubectl cluster-info
kubectl get nodes
Diagram/Architecture:-




Practical : 10 : Scaling in Kubernetes 
Aim:-
To demonstrate horizontal scaling of containerized applications in Kubernetes by creating a Deployment, manually scaling the number of pod replicas up and down, verifying self-healing capabilities by deleting a pod and observing automatic replacement, and exposing the application as a service accessible from the local browser.

Theory:-
Kubernetes enables horizontal scaling of containerized applications by increasing or decreasing the number of pod replicas in response to varying workloads — a fundamentally more flexible approach than vertical scaling. Scaling can be done manually via kubectl scale, or automatically using the Horizontal Pod Autoscaler (HPA) based on CPU utilization, the Vertical Pod Autoscaler (VPA) for resource adjustments, or the Cluster Autoscaler for node-level scaling. Kubernetes continuously monitors the desired cluster state defined in Deployment specifications and reconciles it with the actual state — if a pod crashes or is deleted, the ReplicaSet controller automatically creates a replacement, providing built-in self-healing. When multiple replicas are running, a Kubernetes Service acts as a stable load balancer, distributing incoming traffic evenly across all healthy pods to prevent bottlenecks and ensure high availability. These capabilities eliminate significant operational burden by enabling applications to scale in seconds and recover from failures automatically in production environments.

Step 1: Start Docker Desktop
Ensure Docker Desktop is running.

Step 2: Start Minikube Cluster
Command: minikube start

Step 3: Verify Kubernetes Cluster
Command: kubectl get nodes

Step 4: Create Deployment YAML File
Created file scaling-deployment.yaml with nginx container configuration.

Step 5: Apply Deployment
Command: kubectl apply -f scaling-deployment.yaml

Step 6: Verify Deployment and Pod
Command:
kubectl get deployments
kubectl get pods

Step 7: Scale Deployment to 3 Replicas
Command: kubectl scale deployment web-deployment --replicas=3

Step 8: Scale Down Deployment
Command: kubectl scale deployment web-deployment --replicas=1

Step 9: Demonstrate Self-Healing
Command: kubectl delete pod web-deployment-d4ffb59c9-f529f (pod name)

Step 10: Expose Deployment as Service
Command:
kubectl expose deployment web-deployment --type=NodePort --port=80

Step 11: Access Application
Command: minikube service web-deployment




Practical : 11 : Prometheus and Grafana
Aim:-
To install and configure Prometheus as a metrics collection system on Windows, set up Windows Exporter to expose system-level metrics, connect Grafana as a visualization dashboard tool with Prometheus as the data source, and create custom dashboards to monitor CPU usage and available memory in real time.

Theory:-
Monitoring is a critical DevOps pillar that involves continuously observing system health, performance, and behavior to detect anomalies, diagnose issues, measure deployment impact, and ensure SLAs are met. Prometheus is an open-source monitoring and alerting toolkit (originally built at SoundCloud, now a graduated CNCF project) that collects metrics as time-series data using a pull model — periodically scraping configured endpoints — and provides PromQL for powerful metric analysis. Grafana is an open-source analytics and visualization platform that connects to data sources like Prometheus, MySQL, and Elasticsearch to provide rich, customizable real-time dashboards for operational visibility. Windows Exporter (formerly wmi_exporter) runs as a Windows service to expose system-level metrics (CPU, memory, disk, network) on port 9182 in a format Prometheus can scrape. Together, Prometheus and Grafana form an industry-standard monitoring stack that enables DevOps teams to proactively detect performance bottlenecks, prevent outages, and make data-driven infrastructure decisions.

PART A: INSTALLATION (Windows Setup)
Step 1: Download Prometheus
Open browser.
Visit official website: https://prometheus.io/download/

Download: prometheus-<latest-version>.windows-amd64.zip
Extract the file to: C:\Prometheus

Step 2: Configure Prometheus
Open: C:\Prometheus\prometheus-3.5.1.windows-amd64 in CMD
Open file: prometheus.yml
Replace content with:
# ===============================
# Global Configuration
# ===============================
global:
  scrape_interval: 15s
  evaluation_interval: 15s

# ===============================
# Alertmanager Configuration
# ===============================
alerting:
  alertmanagers:
    - static_configs:
        - targets: []

# ===============================
# Rule Files (Optional)
# ===============================
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# ===============================
# Scrape Configurations
# ===============================
scrape_configs:

  # -------------------------------
  # Prometheus Self Monitoring
  # -------------------------------
  - job_name: "prometheus"

    static_configs:
      - targets: ["localhost:9090"]
        labels:
          app: "prometheus"

  # -------------------------------
  # Node Exporter Monitoring
  # -------------------------------
  - job_name: "node"

    static_configs:
      - targets: ["localhost:9100"]

Step 3: Start Prometheus
Open PowerShell.
Navigate to folder: cd C:\Prometheus\prometheus-3.5.1.windows-amd64
Run: .\prometheus.exe
If configuration is correct, the message appears:
Step 4: Verify Prometheus
Open browser.
Go to: http://localhost:9090
In query box type: up
Click Execute.
If value shows 1, Prometheus is working successfully.

PART B - Installation and Configuration of Node Exporter (Windows)
Step 1: Download Windows Exporter
Open browser.
Visit official GitHub releases page:
https://github.com/prometheus-community/windows_exporter/releases
Under the latest release, scroll to Assets.
Download: windows_exporter-<latest-version>-amd64.msi

Step 2: Install Using MSI Installer
Double-click the downloaded .msi file.
Click Next.
Keep default settings.
Click Install.
Click Finish.
By default, this will: Install Windows Exporter as a Windows Service
Start the service automatically
Run on port 9182

Step 3: Verify Windows Exporter Service
Open PowerShell and run: sc query windows_exporter
If running, you will see: STATE : RUNNING
Step 4: Verify Metrics Endpoint
Open browser and go to: http://localhost:9182/metrics

Step 5: Configure Prometheus to Scrape Windows Exporter
Open: prometheus.yml
Add the following job inside scrape_configs:

Step 6: Restart Prometheus
Stop Prometheus (Ctrl + C) and start again: .\prometheus.exe
Step 7: Verify in Prometheus
Open: http://localhost:9090

Part C – Grafana Installation & Dashboard Creation
Step 1: Download Grafana
Open browser.
Visit official website: https://grafana.com/grafana/download

Select:
OS: Windows
Package: Installer (.msi)
Download the latest version.

Step 2: Install Grafana
Double-click the downloaded .msi file.
Click Next.
Keep default settings.
Click Install.
Click Finish.
Grafana will:
Install as a Windows Service
Start automatically





Step 3: Open Grafana Web Interface
Open browser: http://localhost:3000
Login with default credentials:
Username: admin
Password: admin

Step 4: Add Prometheus Data Source
Click Connections
Click Data Sources
Click Add Data Source
Select Prometheus
In URL field enter: http://localhost:9090
Click Save & Test



For these you need to keep running the  .\prometheus.exe in cmd 

Step 5: Create CPU Usage Dashboard
Click Dashboards.
Click New → New dashboard.
Click Add visualization.
Select Prometheus as a data source.
In the query box, enter:
100 - (avg by (instance) (rate(windows_cpu_time_total{mode="idle"}[1m])) * 100)
Click Run queries.
Select visualization type: Time series.
Set Panel Title: CPU Usage (%)
Under Field settings, set Unit to: Percent (0–100)
Click Apply.






Step 6: Create Memory Usage Panel (same like we did for CPU Usage)
Click Add visualization.
Select Prometheus.
Enter the query: windows_memory_available_bytes / 1024 / 1024 / 1024
Click Run queries.
Select visualization type: Time series.
Set Panel Title: Available Memory (GB)
Set Unit to: Gigabytes (GB)
Click Apply.
Step 7: Save Dashboard
Click Save dashboard.
Enter dashboard name: Grafana Practical
Click Save



Diagram/Architecture:-


Conclusion:-
This practical demonstrated a complete monitoring stack setup using Prometheus and Grafana, enabling real-time visualization of CPU and memory metrics. Effective monitoring provides the feedback loop necessary for continuous improvement and proactive issue detection in DevOps workflows.









Practical : 12 : ELK Stack
Aim:-
To install and configure the ELK Stack (Elasticsearch, Logstash, and Kibana) on Ubuntu running through Windows Subsystem for Linux (WSL), generate and ingest test log data, create a data view in Kibana, and visualize log data using the Discover interface — thereby understanding centralized log management and analysis in a DevOps environment.

Theory:-
The ELK Stack is a collection of three open-source tools by Elastic — Elasticsearch, Logstash, and Kibana — that together provide a comprehensive solution for centralized log collection, storage, search, and visualization in real time. Elasticsearch is a distributed RESTful search engine built on Apache Lucene that stores and indexes log data as JSON documents for fast full-text search; Logstash is a data processing pipeline that ingests logs from multiple sources, transforms them using filter plugins, and forwards them to Elasticsearch; and Kibana provides a browser-based UI for searching, charting, and building dashboards over the stored data. In modern distributed systems where dozens of services generate logs simultaneously, the ELK Stack solves the problem of fragmented logs by centralizing them in one place — enabling instant search across millions of entries, real-time error alerting, and historical trend analysis. Optional lightweight agents like Filebeat and Metricbeat can further streamline log and metric forwarding directly to Elasticsearch or Logstash. Combined with Prometheus and Grafana for metrics monitoring, the ELK Stack completes the observability triad — metrics, logs, and traces — essential for operating reliable, scalable DevOps systems.

Step 1:
Open PowerShell
Open Windows PowerShell as Administrator.
Step 2:
Run the command: wsl --install
Step 3: Check Installed Linux Distributions
Run: wsl -l -v

Step 4: Start Ubuntu
Run the command: wsl -d Ubuntu
Step 5: Verify Ubuntu Terminal
You will see the Ubuntu prompt like: ishika@LAPTOP:~$
Step 6: Update Package List
Run the command: sudo apt update

Step 7: Install Java Development Kit
Run the command: sudo apt install openjdk-11-jdk -y

Step 8: Verify Java Installation
Run the command: java -version

Step 9: Download Elasticsearch Package
Run the command: 
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.11.0-amd64.deb

Step 10: Install Elasticsearch Package
Run the command in the Ubuntu terminal:
sudo dpkg -i elasticsearch-8.11.0-amd64.deb

Step 11: Start Elasticsearch Service
Run the command in the Ubuntu terminal:
sudo service elasticsearch start

Step 12: Check Elasticsearch Using Curl
Run the command: curl http://localhost:9200
Step 13: Check Elasticsearch Service Status
Run the command: sudo systemctl status elasticsearch	
Example output:
elasticsearch.service - Elasticsearch
Active: active (running)

Step 14: Run Password Reset Command
Execute the following command to reset the password of the elastic superuser:
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic

Step 15: Verify Elasticsearch Using the New Password
Run the command:
curl -k -u elastic:<password> https://localhost:9200

Step 16: Download Logstash Package
Run the following command to download Logstash:
wget https://artifacts.elastic.co/downloads/logstash/logstash-8.11.0-amd64.deb

Step 17: Install Logstash Package
Run command: sudo dpkg -i logstash-8.11.0-amd64.deb
Step 18: Check Logstash Version
Run command: /usr/share/logstash/bin/logstash --version

Step 19: Download Kibana Package
Run command: 
wget https://artifacts.elastic.co/downloads/kibana/kibana-8.11.0-amd64.deb
Step 20: Verify the Package is Downloaded
The file kibana-8.11.0-amd64.deb will be saved in the current directory.

Step 21: Install Kibana Package
Run command: sudo dpkg -i kibana-8.11.0-amd64.deb
Step 22: Start Kibana Service
Run command: sudo service kibana start

Step 23: Generate Enrollment Token for Kibana
Run command: 
sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

Step 24: Open Kibana in Browser
Paste in browser: http://localhost:5601

Step 25 : Get Kibana Verification Code
Run Command : sudo journalctl -u kibana.service | grep code


Step 26: Enter Username : elastic
Step 27: Enter Password : Use the generated Elasticsearch password.(Which you got on step 14)

Step 28: Generate a Test Log
Run Command : logger "This is a test log from ELK practical"

Step 29: Send Log Data to Elasticsearch
Run Command : curl -k -u elastic:<password> -X POST https://localhost:9200/logs/_doc -H "Content-Type: application/json" -d '{"message":"ELK practical test log"}'

Step 30: Go to Stack Management
Click the ☰ menu and navigate to:
Stack Management → Data Views

Step 31: Create a New Data View
Click Create data view.
Step 32: Enter Data View Details

Step 33: Open Discover
Go to: Analytics → Discover

Step 34: Select Data View
Select the logs data view.
Step 35: Refresh Logs
Click Refresh to view the newly generated log.
