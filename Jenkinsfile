pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
	stage('Manual Approval') {
	    steps {
		input message: 'Lanjutkan ke tahap Deploy? Klik Proceed (melanjutkan eksekusi pipeline ke tahap Deploy) atau Abort (menghentikan eksekusi pipeline)'
	    }
	}
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
		sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
