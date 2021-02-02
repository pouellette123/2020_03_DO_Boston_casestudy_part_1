pipeline {
    agent any
    environment {
        APP_HOME = "$JENKINS_HOME/workspace/2020_03_DO_Boston_casestudy_part_1/2020_03_DO_Boston_casestudy_part_1/"
        DOCKER_HUB_REPO = "pouellette123/capstone"
        CONTAINER_NAME = "capstone"
    }
    stages {
        stage('Clean Up') {
            steps {
                sh 'rm -rf $APP_HOME'
            }
        }
        stage('Git Clone Repository') {
            steps {
                sh 'git clone https://github.com/pouellette123/2020_03_DO_Boston_casestudy_part_1'
            }
        }
        stage('Build the Docker Image') {
            steps {
                sh 'docker image build -t $DOCKER_HUB_REPO:latest $APP_HOME/'
              //  sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER//'
            }
        }
        stage('Run the Container') {
            steps {
                script {
                    sh 'if (docker ps | grep $CONTAINER_NAME); then docker stop $CONTAINER_NAME;fi'
                    sh 'if (docker image ls | grep $CONTAINER_NAME); then docker rm $CONTAINER_NAME;fi'
                    sh 'docker run --name $CONTAINER_NAME -d -p 8079:8079 $DOCKER_HUB_REPO'
                    //sh 'docker ps | grep $CONTAINER_NAME'
                    //sh 'STATUS = $?'
                    //if ( STATUS == "1" ) {
                    //    sh 'echo if'
                    //    sh 'docker run --name $CONTAINER_NAME -d -p 8079:8079 $DOCKER_HUB_REPO'
                    //} else {
                    //    sh 'echo else'
                    //}
                    //sh 'STAT = $?'
                    //sh 'echo $STAT'
                    //if ($BUILD_NUMBER == 1) {
                    //    sh 'echo running'
                    //}
                    //else {
                     //   sh 'echo not running'
                    //}
                }
            }
        }
    }
}
