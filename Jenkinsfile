pipeline {
    agent any
    stages{
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