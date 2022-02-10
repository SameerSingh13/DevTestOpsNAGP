pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'MAVEN3'
    }

    stages {
        stage('Cloning project from git') {
            steps {
		   // Get some code from a GitHub repository
                git 'https://github.com/SameerSingh13/DevTestOpsNAGP.git'
            }
        }

        stage('Code build') {
            steps {
                // Run Maven on a Unix agent.
                bat "mvn install"
            }

        }

        stage('Unit test') {
            steps {
                // Run Maven on a Unix agent.
                bat "mvn test"
            }

        }
	    
        stage('SonarQube analysis') {
		 steps {
                withSonarQubeEnv('Sonar') { 
                bat "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar"
                }
            }
        }
	    
        stage("Quality gate") {
      steps {
          waitForQualityGate abortPipeline: false
            }
        }
	    
	  stage("final result"){
      steps{
          bat "echo success"
            }
        }
    }

}
