pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                git url: 'https://github.com/AhmedZeins/BackEnd-App-final-task.git' , branch: 'main'
                withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
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
                sh """
                ls
                docker login -u ${USERNAME} -p ${PASSWORD}
                kubectl apply -f /var/jenkins_home/workspace/Finall/NS.yaml
                kubectl apply -f /var/jenkins_home/workspace/Finall/SA.yaml
                kubectl apply -f /var/jenkins_home/workspace/Finall/app.yaml
                kubectl apply -f/var/jenkins_home/workspace/Finall/lba.yaml
                """
                }
            }
        }
    }
}
