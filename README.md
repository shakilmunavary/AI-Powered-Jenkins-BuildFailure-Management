---

#                    **AI-Powered Jenkins Build Failure Management Tool**  


## **🚀 Introduction**  
Managing Jenkins pipeline failures manually is time-consuming. This tool automates **failure detection, troubleshooting, and fixing using AI-powered recommendations**, making DevOps workflows more efficient with less manual effots.

![image](https://github.com/user-attachments/assets/c76027f7-b64b-4556-97f0-97d305bc9f46)

## **🔑 Key Features**
✅ **Automated Build Failure Detection** – Identifies failed Jenkins builds.  
✅ **AI-Powered Error Analysis** – Uses Mistral AI to analyze logs and suggest fixes.  
✅ **Smart Jenkinsfile Corrections** – Extracts AI-suggested fixes and applies them.  
✅ **One-Click Fix Application** – Pushes AI-generated Jenkinsfile updates to GitHub automatically.  
✅ **Enhanced UI** – Displays AI recommendations and toggles for error logs.  

---

## **🛠 Prerequisites**
Before installing, ensure you have the following:
- **Ubuntu Server**
- **Jenkins installed**
- **GitHub repository with a Jenkinsfile**
- **GitHub API token**
- **Mistral AI API key**
- **Node.js installed**

---

## **📥 Installation Guide**
### **1️⃣ Install Jenkins on Ubuntu**
#### **Step 1: Update and Install Java**
```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
java -version  # Verify installation
```
#### **Step 2: Install Jenkins**
```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```
#### **Step 3: Start & Enable Jenkins**
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
#### **Step 4: Access Jenkins**
Navigate to:
```
http://yourIP:8080/
```
Retrieve the admin password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Follow the UI prompts to complete the setup.

---

### **2️⃣ Generate API Token for Jenkins**
- **Login to Jenkins**
- Navigate to **Manage Jenkins > Manage Users**
- Click your username and go to **Configure**
- Under **API Token**, click **Add new Token** and save it.

---

### **3️⃣ Setup GitHub Repository & API Token**
#### **Step 1: Create a GitHub Repository**
- Go to **GitHub** and create a repository.
- Add a **Jenkinsfile** inside the repository.

#### **Step 2: Generate GitHub Token**
- Go to **GitHub > Developer Settings > Personal Access Tokens**
- Click **Generate new token** with the following permissions:
  - `repo`
  - `workflow`
  - `admin:repo_hook`
- Save the token securely.

---

### **4️⃣ Get Mistral AI API Key**
- Visit **[Mistral AI](https://mistral.ai/)**
- Sign in and navigate to **API Keys**
- Generate a new API key and store it securely.

---

### **5️⃣ Clone and Setup the Node.js Application**
#### **Step 5: Clone Node.js Files from GitHub**
```bash
git clone https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management.git
cd AI-Powered-Jenkins-BuildFailure-Management/nodeJs
```

#### **Step 6: Install Dependencies**
```bash
npm install
```

#### **Step 7: Start the Server**
```bash
node app.js
```

---

## **⚙️ Setting Up Environment Variables**
Create two environment files with credentials:

#### **`.env`**
```bash
JENKINS_URL=http://yourIP:8080/
JENKINS_USER=xyz
JENKINS_API_TOKEN=yourJenkinsToken
JENKINS_JOB_NAME=SimpleTomcatApplication
GITHUB_REPONAME=YourRepoWhereYouHaveJenkinsFile
GITHUB_TOKEN=gitHubApiToken
GITHUB_OWNERNAME=gitHubRepoOwnerName
```
#### **`.env.mistral.ai`**
```bash
MISTRAL_API_KEY=YourMistralApiKey
```

---

## **📂 Project Directory Structure**
```
AI-Powered-Jenkins-BuildFailure-Management/
│── jenkins_logs/              # Stores logs and AI-generated Jenkinsfile fixes
│── .env                        # Stores Jenkins & GitHub credentials
│── .env.mistral.ai              # Stores Mistral AI credentials
│── nodeJs/                      # Contains app.js and index.ejs
│    ├── app.js                  # Main backend logic
│    ├── index.ejs                # Frontend UI for displaying builds & AI recommendations
│── package.json                  # Dependencies & metadata
│── README.md                     # Documentation
```

---

## **📡 How It Works**
### **1️⃣ Fetch Failed Builds**
- Retrieves failed builds from Jenkins.

### **2️⃣ Download Error Logs**
- Stores logs for AI analysis.

### **3️⃣ Fetch Existing Jenkinsfile**
- Retrieves pipeline configuration from GitHub.

### **4️⃣ Analyze & Recommend Fixes**
- AI suggests optimized Jenkinsfile updates.

### **5️⃣ Apply AI Fix**
- One-click commit of recommended fixes to the repository.

---

## **🖼️ WebUI Screen**
```
                  ![image](https://github.com/user-attachments/assets/aa18b3f5-84af-4d8c-88ff-b62c01d6e12a)
    
```

---

## **🔎 Troubleshooting**
### ❌ **Jenkins API Authentication Issue**
- Ensure **valid API token** is generated in Jenkins.

### ❌ **AI Fix Not Generated**
- Verify `.env.mistral.ai` contains the correct **Mistral API Key**.
- Ensure logs are **available** for AI analysis.

### ❌ **Fix Not Applied to GitHub**
- Ensure `GITHUB_TOKEN` has **repo access permissions**.
- Verify the repository contains a **Jenkinsfile**.

---

