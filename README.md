# Inventory Management App (Node.js DevOps Demo)

## Description
A simple Node.js-based inventory app demonstrating a DevOps pipeline using Git, GitHub, Jenkins, and Docker.

## Usage

### Run Locally
```bash
npm install
npm start
```

### Docker
```bash
docker build -t inventory-app .
docker run -p 3000:3000 inventory-app
```

### Jenkins
Use the follwing jenkins pipeline in a project.
```groovypipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/pborade90/inventory-node-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker compose build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker compose down --remove-orphans'
                sh 'docker compose up -d'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
```
