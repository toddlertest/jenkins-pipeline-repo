pipeline{
   agent{
     label 'test_node_label'
   }
   options{
     buildDiscarder(logRotator(numToKeepStr: '10'))
   }

   stages{
     stage('Pull from Git'){
       steps{
         git url: "git@github.com:marcelbirkner/selenium2-maven-project.git"
       }
     }
     stage('Create docker container'){
      steps{
        sh 'docker run -d -p 4444:4444 -v /dev/shm:/dev/shm --name selenium-grid selenium/standalone-firefox'
      }
     }
    stage('Run tests'){
      steps{
        sh 'mvn clean test -Dgrid.server.url=http://localhost:4444/wd/hub'
      }
    }
    stage('Remove docker container'){
      sh 'docker rm -f selenium-grid'
    }
   }
}
