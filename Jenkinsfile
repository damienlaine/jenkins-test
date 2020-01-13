
pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "damienlaine/test-jenkins"
        DOCKER_HUB_CRED = "docker-hub-credentials"
    }

    stages{

        stage ('Cloning from GitHub'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
            }
        }

        stage('Master branch'){
            when{
                branch 'master'
            }
            steps {
                echo 'Publishing latest'
                script {
                    def image = docker.build(env.DOCKER_HUB_REPO)
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
                    customImage.push('latest')
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

    }// end stages
}