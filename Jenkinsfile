pipeline {
  // This pipeline requires the following plugins:
  // * Git: https://plugins.jenkins.io/git/
  // * Workflow Aggregator: https://plugins.jenkins.io/workflow-aggregator/
  // * JUnit: https://plugins.jenkins.io/junit/
  // * Claim: https://plugins.jenkins.io/claim/
  agent any  
  stages {
    stage('Example') {
      steps {
        echo 'Example..'
        // sh 改為 bat !!
        // bat 'mvn clean test install'
      }
    }
    stage('Build') {
      steps {
        echo 'Building..'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing.. GitLab Trigger 03:57 !'
        //sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')               
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying....'
        // sh 改為 bat !!
      }
    }    
    stage("Publish NUnit Test Report") {
      steps {
        nunit testResultsPattern: 'TestResult.xml'
        }
    }
  }
  
  // for Config File Provider 程式
  // configFileProvider([configFile(fileId: 'maven-global-settings', 
  // variable: 'MAVEN_GLOBAL_ENV')]) {
  //// sh 改為 bat !!
  //       bat "mvn -s $MAVEN_GLOBAL_ENV clean install"
  // }
  
  // for Pyenv Pipeline 程式
  // withPythonEnv('/usr/bin/python') {
  //// sh 改為 bat !!
  //   bat 'python --version'
  // }
  
  tools {
      maven 'mvn-3.5.4'
  }
  
  post {
          always{
                 echo 'posting....'
                 junit testResults: "**/target/junit-report/junit-report.xml"
                 junit testResults: "**/target/surefire-reports/surefire-reports.xml"
            
                 script{ allure includeProperties: false, jdk: '', properties: [], reportBuildPolicy: 'ALWAYS', results: [[path: 'target/allure-results']] }
                }          
 
          
        }
  
}
