pipeline {
    agent {
        kubernetes {
          label 'cache_test'
          defaultContainer 'jnlp'
          yaml """
    apiVersion: v1
    kind: Pod
    metadata:
      labels:
        some-label: some-label-value
    spec:
      containers:
      - name: maven
        image: maven:3.3.9-jdk-8-alpine
        command:
        - cat
        tty: true
        volumeMounts:
        - mountPath: /cache
          name: maven-cache
      nodeSelector:
        mvncache: true
      volumes:
      - name: maven-cache
        nfs:
          server: fs-d8a1c638.efs.us-east-1.amazonaws.com
          path: "/"
    """
        }
      }
   
    stages {
        stage('Run maven') {
            steps {
               
                container('maven') {
                  
                    //sh 'cd kubernetes;mvn install -Dmaven.test.skip=true'
                    sh 'cd kubernetes;mvn install -Dmaven.repo.local=/cache/java123 -Dmaven.test.skip=true'
                   
                }
            }
        }
    }
}
