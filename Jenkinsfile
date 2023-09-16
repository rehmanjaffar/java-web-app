pipeline {
  agent any
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  stages {
    stage('Build') {
      steps {
        sh './mvnw clean install'
      }
    }
    // stage('Upload to Artifactory') {
    //     steps {
         
    //       // Pull the image using ctr or another containerd CLI tool
    //       sh ' /usr/bin/ctr image pull releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
          
    //       // Run the container and execute commands
    //       sh ' /usr/bin/ctr run --rm releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0 mycontainer jfrog rt upload --url http://74.235.136.21:8081/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/demo-0.0.1-SNAPSHOT.jar java-web-app/'
    //     }
    //   }
stage('Upload to Artifactory') {
      agent {
        docker {
          image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
          reuseNode true
        }
      }
      steps {
        sh 'jfrog rt upload --url http://74.235.136.21:8081/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/demo-0.0.1-SNAPSHOT.jar java-web-app/'
      }
    }
  }
}
