# TravelMemory — MERN Application Deployment on AWS EC2

## 1. Project Overview

TravelMemory is a full-stack web application built using the MERN stack:

- **MongoDB:** Database for storing travel information
- **Express.js:** Backend API framework
- **React.js:** Frontend user interface
- **Node.js:** Backend JavaScript runtime
- **AWS EC2:** Cloud server used to host the application

### Project Objectives

- Deploy a MERN application on an AWS EC2 Ubuntu instance.
- Configure Node.js and npm.
- Connect the backend to MongoDB.
- Deploy and test the backend API.
- Deploy and test the React frontend.
- Configure network access and troubleshoot deployment issues.
- Document the deployment process and verification results.

## 2. Architecture

```text
                 User Browser
                      |
                      v
             React Frontend
                Port 3000
                      |
                HTTP API Calls
                      |
                      v
             Express Backend
                Port 3001
                      |
                      v
                  MongoDB

       Hosting: AWS EC2 Ubuntu Instance
```

The React frontend communicates with the Express backend, which retrieves and manages travel data in MongoDB.

## 3. Prerequisites

- AWS account
- EC2 Ubuntu instance
- SSH key pair
- Node.js and npm
- Git
- MongoDB connection string
- GitHub account and repository

## 4. EC2 Instance Setup

1. Launch an Ubuntu EC2 instance.
2. Configure an SSH key pair.
3. Configure the security group for SSH and the application ports required for testing.
4. Connect to the instance:

```bash
ssh -i "your-key.pem" ubuntu@YOUR_EC2_PUBLIC_IP
```

5. Update the package list:

```bash
sudo apt update
sudo apt upgrade -y
```

## 5. Install Node.js and Git

Verify whether the required tools are installed:

```bash
node --version
npm --version
git --version
```

If Node.js is missing, install a supported version using the official Node.js installation instructions, then verify the versions again.

## 6. Clone the Project

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd TravelMemory
```

If the project has already been cloned, navigate to the existing project directory instead.

## 7. Configure the Backend

Navigate to the backend directory:

```bash
cd backend
npm install
```

Configure the MongoDB connection string using environment variables. Do not commit credentials or `.env` files to GitHub.

Start the backend:

```bash
npm start
```

Verify the API from the EC2 instance:

```bash
curl -i http://localhost:3001/trip
```

A successful response should return an HTTP response containing JSON data.

## 8. Configure and Deploy the Frontend

Navigate to the frontend directory containing `package.json`.

Install dependencies:

```bash
npm install
```

Configure the backend API URL to use the EC2 public IP or the appropriate deployment hostname, rather than `localhost` in the remote user's browser.

For a React development-server demonstration:

```bash
HOST=0.0.0.0 npm start
```

Confirm that the frontend starts successfully and that the browser can reach the backend API.

For a production deployment, build the React application and serve the generated files through a web server such as Nginx.

## 9. Network and Security Configuration

For the initial demonstration, configure the EC2 security group to permit the required application ports from an appropriate source.

- Port 22: SSH administration
- Port 3000: React development server, if used
- Port 3001: Express API, if exposed directly

Restrict SSH access to trusted IP addresses. Avoid exposing MongoDB directly to the public internet.

For a production deployment, use HTTPS and a reverse proxy, and avoid exposing the development server.

## 10. Testing and Verification

Verify the following:

1. The EC2 instance is running.
2. Node.js and npm are installed.
3. The backend starts without errors.
4. The MongoDB connection succeeds.
5. The `/trip` API endpoint returns the expected response.
6. The frontend loads in a browser.
7. The frontend can retrieve travel data from the backend.
8. CORS and network access are configured correctly.

Record the actual test results and attach screenshots.

## 11. Troubleshooting

### Port Already in Use

Error: `EADDRINUSE`

Check the process using the backend port:

```bash
sudo lsof -i :3001
```

Test whether the existing backend is responding:

```bash
curl -i http://localhost:3001/trip
```

### GitHub Push Rejected

Error: `fetch first`

Fetch the remote repository and inspect the branch history before merging. Avoid force-pushing over existing repository history.

### CORS Error

Confirm that the backend permits requests from the actual frontend origin and that the frontend is configured with the correct backend URL.

### MongoDB Connection Error

Verify the connection string, database permissions, network access, and environment variable configuration. Never publish database credentials in the repository.

## 12. Deployment Details

- **GitHub Repository:** https://github.com/Chandhini2/merncapstone
- **Cloud Provider:** AWS
- **Compute:** Amazon EC2
- **Operating System:** Ubuntu
- **Application Stack:** MERN
- **Frontend Port:** 3000, if using the development server
- **Backend Port:** 3001

Live application URL: [Add the verified working URL here]

## 13. Learning Reflection

This project helped me understand the practical steps involved in deploying a MERN stack application on AWS EC2. I gained experience with Linux commands, Node.js configuration, MongoDB connectivity, backend API verification, frontend-backend communication, security group configuration, and GitHub version control.

One challenge I encountered was the `EADDRINUSE` error when the backend attempted to use port 3001 while another process was already listening on that port. I learned to inspect active processes and test the existing API before restarting services. I also encountered GitHub authentication and branch synchronization issues while publishing the project to my own repository.

In future improvements, I would configure a process manager such as PM2, use Nginx as a reverse proxy, enable HTTPS, keep secrets outside source control, and automate deployments through a CI/CD pipeline.

## 14. Evidence

Attached screenshots showing the actual EC2 configuration, Node.js installation, successful MongoDB connection, API response, frontend application, and completed course checks.

Live Application

Frontend URL: http://100.31.72.195:3000

Backend API: http://100.31.72.195:3001/trip


Instance State:

<img width="959" height="472" alt="image" src="https://github.com/user-attachments/assets/87ffefba-97fa-453e-b890-b0d91708e60f" />


Security Group:

<img width="956" height="388" alt="image" src="https://github.com/user-attachments/assets/ee7f2263-6c49-47d4-9e05-ac51d75f3636" />


Frontend API:

http://100.31.72.195:3000/

<img width="959" height="451" alt="image" src="https://github.com/user-attachments/assets/8ff961c2-a240-484f-a92b-f64916390d30" />

Backend API:

http://100.31.72.195:3001/trip

<img width="959" height="472" alt="image" src="https://github.com/user-attachments/assets/ffb119b5-9af3-4ede-b21d-facf804a300c" />


Terminal output:

<img width="959" height="505" alt="image" src="https://github.com/user-attachments/assets/07c9bcf4-4921-490d-82a2-cd1264ef7a20" />

Terminal Backend API response:

<img width="966" height="503" alt="image" src="https://github.com/user-attachments/assets/c8ed91e3-5634-4301-a7cf-a62bc83e7d2b" />


Mongo DB Connection:

<img width="959" height="489" alt="image" src="https://github.com/user-attachments/assets/a7a972db-84cc-47e4-a224-8733b620b6e9" />


Output screenshot of travel experience:

<img width="959" height="460" alt="image" src="https://github.com/user-attachments/assets/f9b34372-78c3-4cd7-bc44-9c0f9f0f9429" />


Refer (mernscreenshot.docx)



