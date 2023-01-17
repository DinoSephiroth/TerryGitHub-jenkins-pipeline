pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    } 
    post {
    always {
      junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true)
    }
  }
}
