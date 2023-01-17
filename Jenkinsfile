pipeline {
  // This pipeline requires the following plugins:
  // * Git: https://plugins.jenkins.io/git/
  // * Workflow Aggregator: https://plugins.jenkins.io/workflow-aggregator/
  // * JUnit: https://plugins.jenkins.io/junit/
  // * Claim: https://plugins.jenkins.io/claim/
  agent 'any'
  
  tools {
    maven 'myMaven'
    }
  
  //options{
    //// This option allows broken builds to be claimed
    //allowBrokenBuildClaiming()
  //}
  
  stages {
    stage('Build') {
      steps {
        echo 'Building..'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing..'
        //sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')               
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying....'
        //sh(script: './mvnw --batch-mode package -DskipTests')
      }
    }    
    stage("Publish NUnit Test Report") {
      steps {
        nunit testResultsPattern: 'TestResult.xml'
        }
    }
  }
}
