pipeline {
    agent any
    options {
		ansiColor("xterm")
	}


    stages {
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
        }
        stage("Deploy"){
            if(env.BRANCH_NAME == 'master'){
            echo "Branch"
        }
}
    }



}