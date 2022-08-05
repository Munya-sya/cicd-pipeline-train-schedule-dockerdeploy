pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps{
                script{
                    app = sudo docker.build("kennedy02/train-schedule-docker-deploy")
                }
            }
        }
        
        
    }
}
