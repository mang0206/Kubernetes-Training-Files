pipeline {
    agent any
    
    environment {
        GIT_URL = "https://github.com/mang0206/indexfile_for_jenkins_test.git"
    }

    stages {
        stage('Pull') {
            steps {
                git url: "${GIT_URL}", 
                    branch: "main", 
                    credentialsId: "for_kubernetice"
            }
        }
        
        stage('docker build and push') {
            steps {
              sh '''
              docker build -t 192.168.1.10:8443/indexfile_for_jenkins_test .
              docker push 192.168.1.10:8443/my_nginx
              '''
            }
        }
        
        stage('deploy kubernetes') {
          steps {
            sh '''
            kubectl create deployment my-nginx --image=192.168.1.10:8443/my_nginx
            kubectl expose deployment my-nginx --type=LoadBalancer --port=8080 \
                                                   --target-port=80 --name=my-nginx-svc
            '''
          }
        }
    }
}
