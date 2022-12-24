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
            steps {
                script {
                    app = docker.build("sramsey822/train-schedule")
                    app.inside {
                        sh 'echo $(curl 192.168.1.20:80)'
                    }
                }
            }
        }
     }
}
