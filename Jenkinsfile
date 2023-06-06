pipeline {
    agent { label 'slave1' }
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh '''
                                docker login -u ${USERNAME} -p ${PASSWORD}
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
