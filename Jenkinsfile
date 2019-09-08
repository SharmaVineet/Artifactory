pipeline {
agent any
   environment {
        Docker_Password = credentials('Docker-Pass')
   }
stages {
   stage('Docker Pull') {
    steps {
     echo "Docker Login"
     sh 'sudo docker login -u pacfisit1989 -p $Docker_Password'
     echo "Docker Pull"  
     sh 'docker pull nginx'
    }
   }
   stage('Docker Run Container')  {
      steps {
         echo "Building Docker Container"
         sh 'docker container run -it -d -p 80:80 nginx'
      } 
   }		
  }
}
