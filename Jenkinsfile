pipeline {
    agent { label 'iti-smart' }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
    } 
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                    if (params.ENV == '${BRANCH_NAME}') {
                        withCredentials([usernamePassword(credentialsId: 'iti-smart-dockerhub', usernameVariable: 'USERNAME_ITI', passwordVariable: 'PASSWORD_ITI')]) {
                            sh '''
                                docker login -u ${USERNAME_ITI} -p ${PASSWORD_ITI}
                                docker build -t 0xze/carrepair${BRANCH_NAME}:v${BUILD_NUMBER} .
                                docker push 0xze/carrepair${BRANCH_NAME}:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > /home/jenkins/build.txt
                                echo ${BRANCH_NAME} > /home/jenkins/branchname.txt
                            '''
                        }
                    }
                    //else {
                      //  echo "user choosed ${params.ENV}"
                    //}
                }
            }
        }
       // stage('deploy') {
         //   steps {
           //     echo 'deploy'
             //   script {
                    //if (params.ENV == "dev" || params.ENV == "test" || params.ENV == "prod") {
               //         withCredentials([file(credentialsId: 'iti-smart-kubeconfig', variable: 'KUBECONFIG_ITI')]) {
                 //           sh '''
                   //             export BRANCH_NAME=$(cat ../branchname.txt)
                     //           mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                       //         cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                         //       rm -f Deployment/deploy.yaml.tmp
                           //     kubectl apply -f Deployment --kubeconfig ${KUBECONFIG_ITI} -n ${BRANCH_NAME}
                            //'''
                      //  }
                   // }
                //}
            //}
        //}
    }
}
