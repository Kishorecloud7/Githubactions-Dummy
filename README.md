<h1>✅ TASK 1: Automate Code Deployment Using CI/CD Pipeline (GitHub Actions) </h1>

<h2>Objective:</h2>

Set up a CI/CD pipeline that automatically <h4>Builds and Deploys a Node.js application</h4> using <h4>GitHub Actions and Docker.</h4>

<h1>🚀 What You Need</h1>

* A GitHub repository

* A Node.js application (simple Express app is fine)

* Docker installed (for local testing)

* GitHub Actions (no setup required, built into GitHub)

<h1>📁 Deliverable</h1>

<h3>Your GitHub repo must contain:</h3>

```
bash

.github/workflows/deploy.yml
```

<h1>🔧 Step-by-Step Implementation</h1>
<h2>1️⃣ Create Project Structure</h2>

<h3>Inside your project folder:</h3>

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

<h3>index.js</h3>

```
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("CI/CD Pipeline Deployed Successfully!");
});

app.listen(port, () => {
  console.log(`App running on port ${port}`);
});

```


<h3>package.json</h3>

```
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

```

<h2>3️⃣ Create Dockerfile</h2>

<h3>Dockerfile</h3>

```
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]

```

<h2>4️⃣ Create GitHub Actions Workflow</h2>

<h3>Create folder + file:</h3>

```
bash
.github/workflows/deploy.yml

```

<h3>Paste this:</h3>

```
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

```


<h1>🎯 Final Output</h1>

<h3>Your repo should contain:</h3>

```
/.github/workflows/deploy.yml
Dockerfile
package.json
index.js

```

<h3>Push code → GitHub Actions automatically runs CI/CD.</h3>
