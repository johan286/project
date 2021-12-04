
pipeline {
    //agent {label 'linux'}
    agent {
        node {
            label 'linux'
            customWorkspace '/tmp/myefs/myworkspace/workspace/declarative_pipeline'
        }
    }

    environment {
    TEST = "radical"
    arr = "[aamir, radical, jordan]"
    hahahah = "Webhook created from pipline"
    }

    stages {
        stage('Git Checkout') {
        steps {
            git branch: 'dev-local-deploy',
                credentialsId: 'git-https-creds',
                url: 'https://gitlab.com/andromeda99/maven-project.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    try {
                        def test1 = "radical1"
                        echo "${TEST}"
                        echo "${test1}"
                        echo "${arr}"
                        echo "${hahahah}"
                        for (int i = 0; i < arr.size(); i++) {
                            sh "echo Hello ${arr[i]}"
                        }

                        sh '/usr/local/src/apache-maven/bin/mvn clean install'
                    } catch(Exception e) {
                        echo "Exception received" + e
                        } 
                }

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
                sh 'sudo sh testing.sh'
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
                sh 'sudo yum install httpd -y'
                sh 'sudo yum install elinks -y'
                sh 'sudo systemctl start httpd'
                sh 'sudo systemctl enable httpd'
                sh 'sudo rm -rf /var/www/html/*'
                sh 'sudo rsync -avt ${WORKSPACE}/webapp/target/webapp /var/www/html'
                sh 'sudo elinks  http://13.59.29.181/webapp/'
                sh 'sudo elinks  http://13.59.29.181/webapp/index_dev.jsp'
                sh 'sudo curl -kv http://13.59.29.181/webapp/index_dev.jsp'

            }
        }
    }
}
