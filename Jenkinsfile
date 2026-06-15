@Library("Shared") _

pipeline {
    agent {
        label "web02"
    }

    stages {

        stage("Code Checkout") {
            steps {
                echo "Cloning source code..."
                code_checkout(
                    "https://github.com/KumarRahulDas/jenkins-shubhamlonde-django-notes-app.git",
                    "dev"
                )
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "Building Docker Image..."
                docker_build("notes-app", "latest", "kuberahul18")
            }
        }

        stage("Push Docker Image") {
            steps {
                echo "Pushing Docker Image..."
                docker_push("notes-app", "latest", "kuberahul18")
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying application..."
                docker_compose()
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }

        failure {
            echo "Deployment Failed!"
        }
    }
}
