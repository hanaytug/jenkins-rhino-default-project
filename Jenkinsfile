pipeline {
    agent { label 'rhino-docker-slave' }
    options { timestamps () }
    stages {
        stage('Fetch') {
            steps {
                git credentialsId: 'github-hanaytug', url: 'git@github.com:hanaytug/jenkins-rhino-default-project.git'
            }
        }
        stage('Renv Restore') {
            steps {
                sh 'printenv'
                sh 'R -e "renv::restore()"'
            }
        }
        stage('Lint R') {
            steps {
                sh 'R -e "rhino::lint_r()"'
            }
        }
        stage('Lint JavaScript') {
            steps {
                sh 'R -e "rhino::lint_js()"'
            } 
        }
        stage('Lint Sass') {
            steps {
                sh 'R -e "rhino::lint_sass()"'
            } 
        }
        stage('Build JavaScript') {
            steps {
                sh 'R -e "rhino::build_js()"'
            } 
        }
        stage('Build Sass') {
            steps {
                sh 'R -e "rhino::build_sass()"'
            } 
        }
        stage('Run R unit tests') {
            steps {
                sh 'R -e "rhino::test_r()"'
            } 
        }
        stage('Run Cypress end-to-end tests') {
            steps {
                dir('.rhino') {
                    sh 'npm run test-e2e'
                }
            }
        }
    }
}
