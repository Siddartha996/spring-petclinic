pipeline{
    agent{label "spc"}
    triggers{
        pollSCM( '* * * * *')
    }
    stages{
        stage('git checkout'){
            steps{
                git url : 'https://github.com/Siddartha996/spring-petclinic.git',
                   branch : 'main'
            }
        }
        //stage('build and scan'){
          //  steps{
            //    withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]){
              //  withSonarQubeEnv('SONAR'){
                //    sh '''mvn package sonar:sonar \
                    //    -Dsonar.projectKey=Siddartha996_spring-petclinic \
                  //      -Dsonar.organization=siddartha996 \
                //        -Dsonar.host.url=https://sonarcloud.io \
              //          -Dsonar.login=$SONAR_TOKEN '''
            //        }
          //      }
        //    }
      //  }
    
       // stage('docker login'){
         //   steps{
           //     withCredentials([usernamePassword(
             //       credentialsId: '44c3b656-1def-4f34-b5d1-ab9c14dfdd61',
                //    usernameVariable: 'DOCKER_USER',
               //     passwordVariable: 'DOCKER_PASS'
              //  )]){
                //    sh '''
               //     echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
             //       '''
           //     }
         //   }
       // }
        stage('docker image push to ecr and pulling from docker hub'){
            steps{
                sh """ docker image pull nginx:1.29 && \
                      aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 069724901154.dkr.ecr.ap-south-1.amazonaws.com && \
                      docker tag nginx:1.29 069724901154.dkr.ecr.ap-south-1.amazonaws.com/dev/spcjava:latest && \
                      docker push 069724901154.dkr.ecr.ap-south-1.amazonaws.com/dev/spcjava:latest """
            }
        }
    }
   // post{
     //   always{
       //     archiveArtifacts artifacts: '**/*.jar'
         //   junit '**/surefire-reports/*.xml'
    //    }
    //}
}
