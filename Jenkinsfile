pipeline {
    agent any 
    
    
    stages{
        stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/umansh/spring-boot-app.git", branch: "main"
            }
        }
        
    }
}
