pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "damienlaine/test-jenkins"
        DOCKER_HUB_CRED = "docker-hub-credentials"
    }

    stages{

        stage ('Clone master and next branches'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
            }
        }

        stage('Master branch'){
            when{
                branch 'master'
            }
            steps {
                echo 'Building from Dockerfile'
                script {
                    def customImage = docker.build($DOCKER_HUB_REPO)
                    def tag = "latest"
                }
            }
        }

        stage('Next branch Docker build'){
            when{
                branch 'next'
            }
            steps {
                echo 'This is next branch, yeah'
            }
        }

        stage('Push to Docker Hub'){
            steps {
                    script {
                        docker.withRegistry('https://registry.hub.docker.com', $DOCKER_HUB_CRED) {
                        customImage.push(${tag})
                    }
                }
            }
        }
    }// end stages
}