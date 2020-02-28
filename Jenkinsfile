node {
    stage('checkout scm'){
    git 'https://github.com/Babita-123/my-new-maven-app'
    }
    
    stage('Compile-Package'){
    sh 'mvn package'
    }
    
    stage('deploy WAR'){
        sshagent(['tomcat-dev']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.19.217.32:/opt/tomcat/webapps'
        }
    }
}
