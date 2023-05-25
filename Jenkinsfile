pipeline { 
  
   agent any

   stages {
   
     stage('Install Dependencies') { 
        steps { 
           sh 'npm install' 
        }
     }
     
     stage('Test') { 
        steps { 
           sh 'echo "testing application..."'
        }
      }

         stage("Deploy nodejs application") { 
         steps { 
           sh 'echo "deploying application..."'
         }

     }
     stage('Build Docker Image') {
        steps {
            script {
                sh 'docker build -t shubham1911/mynodejsapp-1.0 .'
            }
        }
     }
     
     stage("Push Docker image") {
        steps {
            script {
                withCredentials([string(credentialsId: 'shubham1911', variable: 'dockerhubpwd')]) {
                    sh "docker login -u shubham1911 -p ${dockerhubpwd}"
                }
                sh "docker push shubham1911/mynodejsapp-1.0"
            }
        }
     }
      stage('Run Docker Container') {
        steps {
            sh 'docker run -d --name mynodejsapp -p 8888:8888 shubham1911/mynodejsapp-1.0'
        }
     }
  
  
   	}

   }
