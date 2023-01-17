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
    stage('Checkout') {
      steps {
        script {
            checkout([$class: 'GitSCM', branches: [[name: '*/failing-test']], userRemoteConfigs: [[url: 'https://github.com/DinoSephiroth/TerryGitHub-jenkins-pipeline.git']]])
        }
      }
    }
    stage('Test') {
      steps {
        sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')
      }
    }
    stage('Package') {
      steps {
        sh(script: './mvnw --batch-mode package -DskipTests')
      }
    }
    
        stage('Integration') {
      junit 'test-results.xml'
    }

    junit 'more-test-results.xml'

    stage('Ignored') {
      withChecks('Integration Tests') {
        junit 'yet-more-test-results.xml'
      }
    }
    
       stage("Publish NUnit Test Report") {
        steps {
            nunit testResultsPattern: 'TestResult.xml'
        }
    }
    
  }
  //post {
    //always {
      // pmd(canRunOnFailed: true,pattern: '**/target/pwd.xml')
      // The testDataPublishers argument allows failed tests to be claimed
      // junit(testDataPublishers: [[$class: 'ClaimTestDataPublisher']], testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true) 
      // junit 'build/reports/**/*.xml'
      //junit(testResults: 'build/reports/**/*.xml', allowEmptyResults : true)       
    //}
  //}
  
}
