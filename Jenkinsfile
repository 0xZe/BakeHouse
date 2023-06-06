pipeline {
    agent { label 'slave1' }
    stages {
         stage('deploy') {
            steps {
                echo 'deploy'
                script {
                        withCredentials([file(credentialsId: 'slave-k8s-kubeconfig', variable: 'KUBECONFIG_ITI')]) {
                            
                                sh '''
                                export BUILD_NUMBER=$(cat /home/jenkins/build.txt )
                                mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                                cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                                rm -f Deployment/deploy.yaml.tmp
                                kubectl apply -f Deployment --kubeconfig ${KUBECONFIG_ITI} -n ${BRANCH_NAME}    
                            '''                   
                    }
                }
            }
        }
    }
}
