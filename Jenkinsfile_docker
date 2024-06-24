pipeline{
  agent any 
  tools{
    maven "maven3.8.4"
  }
  stages{
    stage('GitClone'){
      steps{
        echo "cloning the lastest applications version"
        git "https://github.com/LandmakTechnology/maven-web-application"
      }
    }
      stage('Test+Build'){
      steps{
        sh "echo Running unitTesting"
        sh "mvn clean package"
        echo "echo test successful and backupArtifacts created"
      }
    }
      stage('codeQuality'){
      steps{
        sh "echo Running detail code analysis"
        sh "mvn sonar:sonar"
        sh  "echo All conditions met/passed"
      }
    }
      stage('upLoadArtifacts'){
      steps{
        sh "echo Running detail code analysis"
        sh "mvn deploy"
        sh "echo backupArtifacts in nexus"
      }
    }
      stage('predeployment'){
      steps{
        sh "echo creating docker image"
        sh "docker build -t mylandmarktech/maven-web-app . "
        sh "docker push mylandmarktech/maven-web-app"
      }
    }
    stage('UnDeploy'){
      steps{
        sh "echo UNDEPLOYING existing application"
        sh "docker rm -f webapp"
      }
    }
    stage('deployment'){
      steps{
        sh "echo application ready for deployment"
        sh "docker run -d -p 8000:8080 --name webapp mylandmarktech/maven-web-app"
      }
    }
  stage('emailNotification'){
    steps{
      sh "echo deployment successful"
    }
  }

  }
}
