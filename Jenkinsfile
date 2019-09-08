pipeline {
agent any
stages {
   stage('Docker Pull') {
    steps {
     echo "Docker Login"
     sh 'docker login -u pacfisit1989 -p Snakes@123t'
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
