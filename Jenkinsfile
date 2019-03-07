pipeline {
    agent {
        kubernetes {
            label 'declarative-pod'
            containerTemplate {
                name 'maven'
                image 'maven:3.3.9-jdk-8-alpine'
                ttyEnabled true
                command 'cat'
                
            }
        }
    }
   
    stages {
        stage('Run maven') {
            steps {
               
                container('maven') {
                  
                    sh 'cd kubernetes;mvn install'
                   
                }
            }
        }
    }
}
