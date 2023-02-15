pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        // checkout source code from your repository
        checkout scm
      }
    }
    stage('Build Docker Image') {
      steps {
        // build a Docker image using a Dockerfile
        sh 'docker build -t my-image .'
      }
    }
    stage('Run Docker Container') {
      steps {
        // run the Docker container and map ports
        sh 'docker run -d -p 8080:8080 --name my-container my-image'
      }
    }
    stage('Deploy Application') {
      steps {
        // deploy the application to the specified IP address
        sh "curl -X POST -H 'Content-type: application/json' -d '{\"container_id\":\"my-container\",\"host\":\"<your_host_ip_address>:8080\"}' http://<your_deploy_script_url>"
      }
    }
  }
  post {
    always {
      // stop and remove the Docker container
      sh 'docker stop my-container || true'
      sh 'docker rm my-container || true'
    }
  }
}
