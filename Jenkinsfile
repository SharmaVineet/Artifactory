pipeline {
agent any
   environment {
        Docker_Pass = credentials('Docker_Password')
        Docker_User = credentials('Docker_Username')
        Version = '1'
        Image_Name = 'mynginx'
   }
stages {
	stage('Docker Login') {
		steps{
			echo "Docker Login"
			sh 'docker login -u $Docker_User -p $Docker_Pass'
		}
	}
	
	stage('Container Cleanup') {
		steps {
			script {
				if [ ! -z $(docker container ps -aq) ] {
					docker container stop $(docker container ps -aq)
					docker container rm $(docker container ps -aq)
				} else {
					echo "There is No Container Running"
				}
			}
		}
	}

	stage('Container Image Cleanup') {
		steps{
			sh 'docker rmi $(docker images -q)'
		}
	}
	
	stage('Docker Build') {
		steps{
			sh 'docker build -t $Docker_User/$Image_Name:$Version .'
		}
	}

	stage('Docker Run') {
		steps{
			sh 'docker container run -it -d -p 80:80 $(docker images $Docker_User/$Image_Name:$Version -q)'
		}
	}
  }
}
