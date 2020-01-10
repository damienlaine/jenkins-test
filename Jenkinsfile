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
        stage ('Switch branches'){
            steps {
                script {
                    def gitBranch = sh script:'git rev-parse --abbrev-ref HEAD', returnStdout: true
                    println "Gitbranch: ${gitBranch}"
                    GIT_BRANCH = gitBranch.replace("/n", "")
                    env.GIT_BRANCH = GIT_BRANCH
                }
                 echo "Current agent  info: ${env.GIT_BRANCH}"
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