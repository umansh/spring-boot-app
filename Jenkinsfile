pipeline {
    agent any 
    tools {
        jdk 'Java17'
        maven 'Maven3'
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
