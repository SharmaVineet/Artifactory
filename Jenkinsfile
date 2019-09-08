pipeline {
agent any
   environment {
        Docker_Pass = credentials('Docker_Password')
        Docker_User = credentials('Docker_Username')
        Image_Name = 'mynginx'
   }
stages {
	stage('Docker Login') {
		steps{
			echo "Docker Login"
			sh 'docker login -u $Docker_User -p $Docker_Pass'
		}
	}
	
#	stage('Container Cleanup') {
#		steps {
#			echo "Stopping Containers"
#			sh 'docker ps -qa|xargs --no-run-if-empty docker container stop'
#			echo "Removing Containers"
#			sh 'docker ps -qa|xargs --no-run-if-empty docker container stop'
#		}
#	}

	stage('Container Image Cleanup') {
		steps{
			sh 'docker images -q| xargs --no-run-if-empty  docker rmi'
		}
	}
	
	stage('Docker Build') {
		steps{
			sh 'docker build -t $Docker_User/$Image_Name .'
		}
	}

	stage('Docker Push') {
		steps{
			sh 'docker push $Docker_User/$Image_Name'
		}
	}
	
	stage('Ansible Run') {
		ansiblePlaybook(
		inventory: /etc/hosts
		playbook: ansiblePlaybook.yml
		)
	}
  }
}
