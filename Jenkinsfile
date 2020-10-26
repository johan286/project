pipeline {
    agent {Label 'slavenode-linux'}
    
    stages {
        stage('Build') {
            steps {
                sh '/usr/local/src/apache-maven/bin/mvn clean install'
            }
        }
        stage('Scanning') {
            steps {
                echo 'Scanning in progress.'
            }
        }
        stage('Testing') {
            steps {
                echo 'Testing..'
                sh 'pwd'
                sh 'sudo scp -i id.rsa -o StrictHostKeyChecking=no -r ${WORKSPACE}/webapp root@testing-webserver:/var/www/html'
            }
        }
        stage('Nexus Upload') {
            steps {
                echo 'Uploading artifact to Nexus.'
            }
        }
        stage('Deployment') {
            steps {
                echo 'Deployment..'
            }
        }
    }
}

