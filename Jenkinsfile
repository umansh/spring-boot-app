pipeline {
    agent any 
    environment {
        tool name: 'Java17', type: 'jdk'
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
