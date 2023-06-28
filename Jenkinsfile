node{
def mavenHome = tool name: 'maven3.9.2'
stage('1.clone'){
  //git "https://github.com/solomanty/maven-web-application"
  git branch: 'development', url: 'https://github.com/solomanty/maven-web-application'
}
stage('2.test and build'){
 sh "${mavenHome}/bin/mvn package"
}
stage('3.CodeQualityAnalysis'){
 sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('4.Artifactory'){
 sh "${mavenHome}/bin/mvn deploy"}
stage('5.deploy2UAT'){
deploy adapters: [tomcat9(credentialsId: 'tomcat-credential', path: '', url: 'http://3.94.146.235:8177/')], contextPath: null, war: 'target/*war'
}
stage('6.approval'){
    sh "echo 'apps ready for review' "
    timeout(time:5, unit: 'HOURS') {
    input message: 'Application ready for deployment, please review and approve'
      }
}      
stage('7.production'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credential', path: '', url: 'http://3.94.146.235:8177/')], contextPath: null, war: 'target/*war'
}
stage('8.notification'){
    emailext body: '''Hello Team,
Please check the pipeline work done.

Solomon Alamutu''', recipientProviders: [buildUser()], subject: 'Build status', to: 'developers'
}
}
  
