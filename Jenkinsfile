node {
    stage('checkout scm'){
    git 'https://github.com/Babita-123/my-new-maven-app'
    }
    
    stage('SonarQube analysis') {
    withSonarQubeEnv('sonar-6') {
    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
    } // submitted SonarQube taskId is automatically attached to the pipeline context
  }
    
    stage("Quality Gate Status Check"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }        
    
    stage('Compile-Package'){
    sh 'mvn package'
    }
    
    
    stage('deploy WAR'){
        sshagent(['tomcat-dev']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@172.31.20.228:/opt/tomcat/webapps'
        }
    }
}
