pipeline {
    agent any

    stages{


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