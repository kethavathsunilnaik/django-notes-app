pipeline {
    agent any
    stages{
        stage("Clone code"){
            steps {
                echo "cloning the code"
                git url:"https://github.com/kethavathsunilnaik/django-notes-app.git", branch:"main"
            }
            
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
                
            }
        }
        stage("Push to DockerHub"){
            steps {
                echo "Pushing the image to DockerHub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                    sh "docker tag my-note-app ${env.DockerHubUser}/my-note-app:version1"
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                    sh "docker push ${env.DockerHubUser}/my-note-app:version1"
                }
                
            }
            
        }
        stage("Deploy"){
            steps {
                echo "Deploy the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
            
        }
    }
}
