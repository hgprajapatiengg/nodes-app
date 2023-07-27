pipeline {
    agent any
     stages{
        
        stage ("code clone from git"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/hgprajapatiengg/nodes-app.git", branch:"master"
            }
            
        }
        stage ("Build"){
            steps {
                echo "Building the Image"
                sh "docker build -t my-notes-app ."
                
            }
            
        }
        stage ("push on docker hub"){
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerhubPass', usernameVariable: 'dockerhubUser')]) {
                sh "docker tag my-notes-app ${env.dockerhubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/my-notes-app:latest"
                }
            }
        }
        stage ("Deploy"){
            steps {
                echo "Deploying container"
                sh "docker-compose down && docker-compose up -d"
                
            }
            
        }
        
        
        
    }
}
