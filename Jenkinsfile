pipeline {
    agent any

    environment {
        TOMCAT_URL  = "http://192.168.1.8:8000"
        APP_NAME    = "my-webapp"
        WAR_FILE    = "target/my-webapp.war"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Fetching code from GitHub..."
                git branch: 'main', url: 'https://github.com/DEEPAKRAJ2002/my-java-webapp'
            }
        }

        stage('Build WAR') {
            steps {
                echo "Running Maven package..."
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                        echo "Deploying WAR to Tomcat..."
                        curl -u $USER:$PASS \
                          --upload-file $WAR_FILE \
                          "$TOMCAT_URL/manager/text/deploy?path=/$APP_NAME&update=true"
                    '''
                }
            }
        }
    }
    post {
          success {
            echo "Deployment successful! Visit: $TOMCAT_URL/$APP_NAME"
          }
          failure {
            echo "Deployment failed. Check logs!"
          }
        }
}
