node{
  def mavenHome = tool name: 'maven3.8.2'
  stage('1Clone'){
    git 'https://github.com/LandmakTechnology/maven-web-application'
  }
  stage('2Test+build'){
    sh "${mavenHome}/bin/mvn clean package"
  }
/*
  stage('SonarQube'){
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('4UploadArtifacts'){
    sh "${mavenHome}/bin/mvn deploy"
  }

  stage('5Deploy'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.166.85.32:8177/')], contextPath: null, war: 'target/*war'
  }
  stage('6Notification'){
    emailext body: '''Hi Team,
Build status
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'
  }
*/
}
