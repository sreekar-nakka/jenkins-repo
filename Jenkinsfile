pipeline {
    agent any
    
    stages {
        stage('Build Application') {
            steps {
                bat 'mvn clean install'
            }
        }
        
        stage('Deploy CloudHub') {
            environment {
                ANYPOINT_CREDENTIALS = credentials('anypointplatform')
            }
            steps {
                echo 'Deploying mule project due to the latest code commit…'
                echo 'Deploying to the configured environment….'
                bat 'mvn clean deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW}'
            }
        }
        
        stage('Ok') {
            steps {
                echo "Ok"
            }
        }
    }
    
    post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}
