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
        stage('docker image push to ecr and pulling from docker hub'){
            steps{
                sh """ docker image pull nginx:1.29 && \
                      aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 069724901154.dkr.ecr.ap-south-1.amazonaws.com && \
                      docker tag nginx:1.29 069724901154.dkr.ecr.ap-south-1.amazonaws.com/dev/spcjava:latest && \
                      docker push 069724901154.dkr.ecr.ap-south-1.amazonaws.com/dev/spcjava:latest """
            }
        }
    }
}
