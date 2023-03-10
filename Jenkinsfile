pipeline {
    agent any
    
    environment {
        GIT_URL = "https://github.com/mang0206/indexfile_for_jenkins_test.git"
    }

    stages {
        stage('Pull') {
            steps {
                git url: "${GIT_URL}", 
                    branch: "main"
            }
        }
        
        stage('docker build and push') {
            steps {
              sh '''
              docker build -t 192.168.1.10:8443/my_nginx .
              docker push 192.168.1.10:8443/my_nginx
              '''
            }
        }
        
        stage('deploy kubernetes') {
          steps {
            sh '''
            kubectl apply -f jenkins_volume.yaml
            kubectl apply -f my_nginx.yaml
            '''
          }
        }
    }
}
