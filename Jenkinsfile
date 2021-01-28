pipeline {
    agent any
    stages {
        stage('Git-Checkout') {
            steps {
                echo "Checking out from git repo!!";
                git branch: 'main', credentialsId: 'a922c94d-8bf9-47fe-9891-864e199424ed', url: 'https://github.com/hitika26/mvn_webapp.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the checked out project!";
                bat 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo "Running JUnit tests!!";
                deploy adapters: [tomcat9(credentialsId: '1058f6c2-4b0b-45aa-8e61-35694052ff0b', path: '', url: 'http://localhost:8081/')], contextPath: 'mvn-webapp', onFailure: false, war: 'target/mvnwebapp.war'
            }
        }
        
        
    }

    post {
        always {
            echo 'This will alwaysw run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
