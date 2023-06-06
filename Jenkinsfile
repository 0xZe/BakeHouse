pipeline {
    agent { label 'iti-smart' }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
    } 
    stages {
        //stage('build') {
          //  steps {
            //    echo 'build'
              //  script{
                    //if (params.ENV == "release") {
                //        withCredentials([usernamePassword(credentialsId: 'iti-smart-dockerhub', usernameVariable: 'USERNAME_ITI', passwordVariable: 'PASSWORD_ITI')]) {
                  //          sh '''
                    //            docker login -u ${USERNAME_ITI} -p ${PASSWORD_ITI}
                      //          docker build -t 0xze/carrepair${BRANCH_NAME}:v${BUILD_NUMBER} .
                        //        docker push 0xze/carrepair${BRANCH_NAME}:v${BUILD_NUMBER}
                          //      echo ${BUILD_NUMBER} > ../build.txt
                            //    echo ${BRANCH_NAME} > ../branchname.txt
                            // '''
                        //}
                    //}
                    //else {
                      //  echo "user choosed ${params.ENV}"
                    //}
              //  }
           // }
       // }
         stage('deploy') {
            steps {
                echo 'deploy'
                script {
                    if (params.ENV == "dev" ) {
                        withCredentials([file(credentialsId: 'iti-smart-kubeconfig', variable: 'KUBECONFIG_ITI')]) {
                            
                             // export BRANCH_NAME=$(cat /home/jenkins/branchname.txt)
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
}
