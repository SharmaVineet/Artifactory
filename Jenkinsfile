pipeline {
agent any
   environment {
        Docker_Pass = credentials('Docker_Password')
        Docker_User = credentials('Docker_Username')
        Version = 1
   }
stages {
	stage('Docker Login') {
		steps{
			echo "Docker Login"
			sh 'docker login -u $Docker_User -p $Docker_Pass'
		}
	}
	
	stage('Container Cleanup') {
		steps{
			sh 'docker container stop $(docker container ps -aq)'
			sh 'docker container rm $(docker container ps -aq)'
		}
	}

	stage('Container Image Cleanup') {
		steps{
			sh 'docker rmi $(docker images -q)'
		}
	}
	
	stage('Docker Build') {
		steps{
			sh 'docker build -t $Docker_User/mynginx:$Version .'
		}
	}

	stage('Docker Run') {
		steps{
			sh 'docker container run -it -d -p 80:80 $(docker images -q)'
		}
	}
  }
}
