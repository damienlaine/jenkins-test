pipeline {
    agent any

    stages{

        stage ('Clone master and next branches'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
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