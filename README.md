<h1>✅ TASK 1: Automate Code Deployment Using CI/CD Pipeline (GitHub Actions) </h1>

<h2>Objective:</h2>

<h4>Set up a CI/CD pipeline that automatically builds and deploys a Node.js application using GitHub Actions and Docker.</h4>

<h1>🚀 What You Need</h1>

* A GitHub repository

A Node.js application (simple Express app is fine)

Docker installed (for local testing)

GitHub Actions (no setup required, built into GitHub)

<h1>📁 Deliverable</h1>

Your GitHub repo must contain:

.github/workflows/deploy.yml

<h1>🔧 Step-by-Step Implementation</h1>
<h2>1️⃣ Create Project Structure</h2>

Inside your project folder:
```
/my-node-app
 ├── Dockerfile
 ├── package.json
 ├── index.js
 ├── .github/
 │   └── workflows/
 │       └── deploy.yml
```
<h2>2️⃣ Sample Node.js App</h2>

index.js

const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("CI/CD Pipeline Deployed Successfully!");
});

app.listen(port, () => {
  console.log(`App running on port ${port}`);
});


package.json

{
  "name": "ci-cd-demo",
  "version": "1.0.0",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}

<h2>3️⃣ Create Dockerfile</h2>

Dockerfile

FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]

<h2>4️⃣ Create GitHub Actions Workflow</h2>

Create folder + file:

.github/workflows/deploy.yml


Paste this:

name: CI/CD Pipeline

on:
  push:
    branches: ["main"]   # Runs pipeline on every push to main branch

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "18"

      - name: Install dependencies
        run: npm install

      - name: Run tests (optional)
        run: echo "No tests added"

      - name: Build Docker image
        run: docker build -t my-node-app .

      - name: Save Docker image as artifact
        uses: actions/upload-artifact@v4
        with:
          name: docker-image
          path: |
            **/Dockerfile



<h1>🎯 Final Output</h1>

Your repo should contain:

/.github/workflows/deploy.yml
Dockerfile
package.json
index.js


Push code → GitHub Actions automatically runs CI/CD.</h3>
