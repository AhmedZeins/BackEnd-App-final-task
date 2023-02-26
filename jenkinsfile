pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                git 'https://github.com/AhmedZeins/BackEnd-App-final-task.git'
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build . -t zeinsss/app:v1.1 --network host
                docker push zeinsss/app:v1.1
                """
                }
            }
        }
         stage('CD') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                git 'https://github.com/AhmedZeins/BackEnd-App-final-task.git'
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                kubectl apply -f /var/jenkins_home/workspace/Final/app.yaml
                kubectl apply -f/var/jenkins_home/workspace/Final/lba.yaml
                """
                }
            }
        }
    }
}
