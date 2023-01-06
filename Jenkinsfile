pipeline{

	agent any


	stages {
	    
	    stage('gitclone') {

			steps {
				 git branch: 'main', url: 'https://github.com/bayeserigneseck40/ProjetSIR2022.git'
			}
		}

		stage('Build') {

			steps {
				bat 'docker build -t projetsir2022/projet2022:groupe2 .'
			}
		}
		
		
		stage('Build tag') {

			steps {
				bat 'docker tag  projetsir2022/projet2022:groupe2  projetsir2022/projet2022:groupe2 '
			}
		}

		stage('Push') {

			steps {
				withDockerRegistry([credentialsId: "docker-hub" ,url:"" ]){
				bat 'docker push projetsir2022/projet2022:groupe2'
				}
			}
		}
		
		stage('Build deployment') {

			steps {
				bat 'kubectl create deployment projetsir2022 --image=projetsir2022/projet2022 '
				bat 'kubectl expose deployment projetsir2022 --type=NodePort --port 8084 '
				
			}
		}
	   }

	post {
		always {
			bat 'docker logout'
		}
	}

}
