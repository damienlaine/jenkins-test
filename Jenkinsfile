
pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "damienlaine/test-jenkins"
        DOCKER_HUB_CRED = "docker-hub-credentials"
    }

    stages{
        stage('Master branch'){
            when{
                branch 'master'
            }
            steps {
                echo 'Publishing latest'
                script {
                    def image = docker.build(env.DOCKER_HUB_REPO)
                    def version = sh """#!/bin/bash
                    awk -v RS='' '/#/ {print; exit}' RELEASE.md | head -1 | sed 's/#//'
                    """
                    echo $version
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
                        image.push($version)
                        image.push('latest')
                    }
                }
            }
        }

        stage('Next branch'){
            when{
                branch 'next'
            }
            steps {
                echo 'This is next branch, yeah'
            }
        }

    }// end stages
}