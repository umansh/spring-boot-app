pipeline {
    agent any
    tools {
        jdk 'java'
        maven 'maven'
    }
    
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/umansh/spring-boot-app.git", branch: "main"
            }
        }
        
    }
}
