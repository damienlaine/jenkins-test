pipeline {
    agent any
    
    stages{
        stage ('Clone master and next branches'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/next']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/damienlaine/jenkins-test.git']]])
            }
        }
        stage ('test'){
            steps {
                echo env.BRANCH_NAME
            }
        }
        stage('master-branch-stuff'){
            when{
                branch 'master'
            }
            steps {
                echo 'run this stage - ony if the branch = master branch'
            }
        }

        stage('dev-branch-stuff'){
            when{
                branch 'next'
            }
            steps {
                echo 'unstable'
            }
        }

    }
}