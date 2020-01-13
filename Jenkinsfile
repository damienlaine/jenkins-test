
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
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
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

        stage('Push to Docker Hub'){
            steps {
                    script {
                        docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
                        customImage.push(${tag})
                    }
                }
            }
        }
    }// end stages
}