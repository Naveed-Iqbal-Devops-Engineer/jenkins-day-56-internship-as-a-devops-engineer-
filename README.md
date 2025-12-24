jenkins-day-56-internship-as-a-devops-engineer
Multibranch CI/CD Pipeline for Three-Tier Application Using Jenkins, Docker Compose & Docker Hub ,

Industry Scenario
You are a DevOps Engineer at a fast-growing tech company that maintains a three-tier full-stack application. The application consists of:
Frontend: React
Backend: Node.js
Database: MongoDB.


The organization wants automated builds and deployments for three environments:
Development (dev) → For developer testing
Staging (stg) → For QA and pre-production validation
Production (prod) → For live users


Your task is to set up a CI/CD pipeline using Jenkins Multibranch Pipeline. Each Git branch corresponds to an environment (dev, stg, prod).

Objective
✔ Configure Jenkins Multibranch Pipeline to detect branches automatically
 ✔ Build Docker images for frontend and backend
 ✔ Push images to three registries:
AWS ECR (primary for deployment)
Docker Hub (public image storage)
GitHub Container Registry (GHCR)
 ✔ Deploy environment-specific Docker Compose stacks on an Ubuntu EC2 instance
 ✔ Use branch-based image tagging for better version control
 ✔ Ensure secure handling of credentials using Jenkins Credentials Store



Architecture Overview
Components:
Source Code Repository: GitHub
Pipeline Engine: Jenkins (Multibranch Pipeline)
Image Registries: AWS ECR, Docker Hub, GitHub Container Registry
Deployment Server: Ubuntu EC2 with Docker & Docker Compose installed


# 🧱 Three-Tier MERN Application

This is a full-stack three-tier web application built with:

- **Frontend**: React + Nginx
- **Backend**: Node.js + Express
- **Database**: MongoDB Atlas (Cloud DB)

---

## 📁 Folder Structure

.
- ├── backend/ # Express.js backend API
- ├── frontend/ # React frontend (served via Nginx)
- ├── docker-compose.yml # Docker Compose configuration file
- └── README.md # Project documentation


### 📥 Step 1: Clone the Repository
- Fork the repository
<pre> git clone https://github.com/&lt;your-username&gt;/&lt;your-repo&gt;.git </pre>
- cd your-repo

# MongoDB Atlas

## 1️⃣ Create a MongoDB Atlas Account
- Go to: https://www.mongodb.com/cloud/atlas
- Sign up (Google/GitHub/Email)
- After login, click "Build a Database"

## 2️⃣ Create Free Cluster
- Choose “Shared” Tier (Free) → Click "Create"
- Cloud Provider & Region: Choose AWS or GCP (select a nearby region)
- Cluster Name: e.g., three-tier-cluster
- Click Create Cluster (takes ~1-2 minutes)

## 4️⃣ Add IP Whitelist
- Go to "Network Access"
- Click “Add IP Address”
- Choose ALLOW ACCESS FROM ANYWHERE (0.0.0.0/0) for now
- You can restrict to your EC2 IP for production

## 5️⃣ Get the Connection String
- Go to Clusters > Connect > Connect your application
- Choose driver: Node.js, version >= 3.6
- Copy the URI:
<pre><code> MONGO_URI="mongodb+srv://&lt;username&gt;:&lt;password&gt;@cluster0.mongodb.net/three-tier-db?retryWrites=true&amp;w=majority" </code></pre>- 
Replace <password> with your actual password.

## 6️⃣ Add Environment Variables
- Create a .env file inside the backend/ folder:

### backend/.env
<pre><code>MONGO_URI="mongodb+srv://&lt;username&gt;:&lt;password&gt;@cluster0.mongodb.net/three-tier-db?retryWrites=true&amp;w=majority" </code></pre>

## 7️⃣ Run the Application
### Backend
<pre>cd backend
node server.js</pre>
#### Frontend

<pre>cd frontend
npm start</pre>

