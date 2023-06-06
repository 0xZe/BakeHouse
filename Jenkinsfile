pipeline {
    agent { label 'iti-smart' }
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                        withCredentials([usernamePassword(credentialsId: 'iti-smart-dockerhub', usernameVariable: 'USERNAME_ITI', passwordVariable: 'PASSWORD_ITI')]) {
                            sh '''
                                docker login -u ${USERNAME_ITI} -p ${PASSWORD_ITI}
                                docker build -t 0xze/bakehouse:v${BUILD_NUMBER} .
                                docker push 0xze/bakehouse:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > /home/jenkins/build.txt
                                echo ${BRANCH_NAME} > /home/jenkins/branchname.txt
                                '''
                    }
                }
            }
        }
    }
}
