
pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "damienlaine/test-jenkins"
        DOCKER_HUB_CRED = "docker-hub-credentials"
        VERSION = ''
    }

    stages{
        stage('Docker build for master branch'){
            when{
                branch 'master'
            }
            steps {
                echo 'Publishing latest'
                script {
                    image = docker.build(env.DOCKER_HUB_REPO)
                    VERSION = sh(
                        returnStdout: true, 
                        script: "awk -v RS='' '/#/ {print; exit}' RELEASE.md | head -1 | sed 's/#//' | sed 's/ //'"
                    ).trim()
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
                        image.push("${VERSION}")
                        image.push('latest')
                    }
                }
            }
        }

        stage('Staging deployment'){
            when{
                branch 'master'
            }
            steps {
                echo "Deployment on staging environment"
                script {
                    def remote = [:]
                    remote.name = "linto-staging"
                    remote.host = "stage.linto.ai"
                    remote.allowAnyHosts = true
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh_stage', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                    remote.user = userName
                    remote.identityFile = identity
                    sshCommand remote: remote, command: 'docker pull ${DOCKER_HUB_REPO}:latest'
                    }
                }
            }
        }

        stage('Docker build for next (unstable) branch'){
            when{
                branch 'next'
            }
            steps {
                echo 'Publishing unstable'
                script {
                    image = docker.build(env.DOCKER_HUB_REPO)
                    VERSION = sh(
                        returnStdout: true, 
                        script: "awk -v RS='' '/#/ {print; exit}' RELEASE.md | head -1 | sed 's/#//' | sed 's/ //'"
                    ).trim()
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_HUB_CRED) {
                        image.push("${VERSION}-unstable")
                        image.push('latest-unstable')
                    }
                }
            }
        }


        stage('Beta deployment'){
            when{
                branch 'next'
            }
            steps {
                echo "Deployment on beta environment"
                script {
                    def remote = [:]
                    remote.name = "linto-beta"
                    remote.host = "beta.linto.ai"
                    remote.allowAnyHosts = true
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh_beta', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                    remote.user = userName
                    remote.identityFile = identity
                    sshCommand remote: remote, command: 'docker pull ${DOCKER_HUB_REPO}:latest-unstable'
                    }
                }
            }
        }

    }// end stages
}