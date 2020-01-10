pipeline {
    agent any
    
    environment {
        GIT_BRANCH = ''
    }

    stages{

        stage ('Clone master and next branches'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
            }
        }

        stage('Build') {
            steps {
                sh 'git status'
            }
        }

        stage ('Switch branches'){
            steps {
                script {
                    TEST = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
                    echo "branche git ${TEST}"
                    env.GIT_BRANCH = TEST
                }
                 echo "Current branch: ${env.GIT_BRANCH}"
            }
        }

        stage('master-branch-stuff'){
            when{
                branch 'master'
            }
            steps {
                echo 'This is master branch, yeah'
            }
        }

        stage('dev-branch-stuff'){
            when{
                branch 'next'
            }
            steps {
                echo 'This is next branch, yeah'
            }
        }

    }
}