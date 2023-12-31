pipeline {
    agent any
    tools {
        jdk 'java'
        maven 'maven'
    }
    environment {
        APP_NAME = "complete-prodcution-e2e-pipeline"
        //RELEASE = "1.0.0"
        DOCKER_USER = "umansh"
        DOCKER_PASS = 'docker'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        //IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
        IMAGE_TAG = "${BUILD_NUMBER}"
        JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")

    }
    
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/umansh/spring-boot-app.git", branch: "main"
            }
        }
        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test Application"){
            steps {
                sh "mvn test"
            }

        }
        stage("static code analysis"){
            steps {
                withSonarQubeEnv(installationName: 'sonar-api', credentialsId: 'sonar-api') {
                    sh 'mvn sonar:sonar'
            }
          }     
        }
        stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }

        }
        stage("Trigger CD Pipeline") {
            steps {
                script {
                    sh "curl -v -k --user admin:${JENKINS_API_TOKEN} -X POST -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' --data 'IMAGE_TAG=${IMAGE_TAG}' 'http://rneix-88-150-100-27.a.free.pinggy.online/job/gitops-complete-pipeline/buildWithParameters?token=gitops-token'"
                }
            }

        }



        
    }
}
