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
			sh 'container_id=`docker container ps -aq`'
			sh 'for container in `echo $container_id`; do echo "Stopping Docker Container ID $container"; docker container stop $container;echo "Removing Docker Container ID $container";docker container rm $container;done;'		
		}
	}

	stage('Container Image Cleanup') {
		steps{
			sh 'image_id=`docker images -q`'
			sh 'for image in `echo $container_id`; do echo "Removing Docker Image ID $image";docker rmi $image;done;'		
		}
	}
	
	stage('Docker Build') {
		steps{
			sh 'docker build -t $Docker_User/mynginx:$Version .'
		}
	}

	stage('Docker Build') {
		steps{
			sh 'image_id=`docker images -q`'
			sh 'docker container run -it -d -p 80:80 $image_id'
		}
	}
  }
}
