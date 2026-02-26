pipeline{
    agent{label "java"}
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
        stage('build and scan'){
            steps{
                withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]){
                withSonarQubeEnv('SONAR'){
                    sh '''mvn package sonar:sonar \
                        -Dsonar.projectkey=Siddartha996_spring-petclinic \
                        -Dsonar.organization=siddartha996 \
                        -Dsonar.host.url=https://sonarcloud.io/ \
                        -Dsonar.login=$SONAR_TOKEN '''
                    }
                }
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: '**/*.jar'
            junit '**/surefire-reports/*.xml'
        }
    }
}