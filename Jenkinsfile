pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo " Cloning the code"
                git url:"https://github.com/Bhim-Kumar/django-notes-app.git", branch:"main"
            }
            
        }
        stage("Build"){
            steps{
                echo " Building the Code "
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                echo " Pushing the code to docker hub "
                withCredentials([usernamePassword(credentialsId:"Docker_Hub",passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){ 
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo " Deploying the code "
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
    }
