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
                    app = docker.build("kennedy02/train-schedule-docker-deploy")
                }
            }
        }
        stage('Push Docker Image') {
            when{
                branch 'master'
            }
            steps{
                script{
                    docker.withRegistry('', docker_hub_login){
                        app.push("${env.BUILD_NUMBER}") 
                        app.push("latest") 
                    }
                }
            }
        }
        
    }
}
