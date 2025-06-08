pipeline{
	agent any
	environment{
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
	}
	tools{
		maven 'Maven'
	}
	stages{
		stage('Checkout'){
			steps{
				git branch:'master',url:'https://github.com/RANI921/Q5.git'
			}
		}
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
		}
		stage('Test'){
			steps{
				sh 'mvn test'
			}
		}
		stage('Archive'){
			steps{
				archiveArtifacts artifacts:'target/*.war',fingerprint:true'
			}
		}
		stage('Deploy'){
			steps{
				sh 'mvn clean package'
				sh 'ansible-playbook ansible/hosts.ini -i ansible/playbook.yml'
			}
		}
	}
	post{
		success{
			echo "Successfull"
		}
		failure{
			echo "Failure"
		}
	}
}
