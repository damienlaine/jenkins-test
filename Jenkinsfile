pipeline {
    agent any

    stages{

        stage ('Clone master and next branches'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
            }
        }

        

        stage('Master branch Docker build'){
            when{
                branch 'master'
            }
            steps {
                echo 'Building latest and Semver images'
                script {
                    def customImage = docker.build("damienlaine/test-jenkins")
                    customImage.push()
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

    }
}