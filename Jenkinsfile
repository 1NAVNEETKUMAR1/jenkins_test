pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN3"
    }

    stages {
	    stage ('scm') {
		    steps {
			    // Get some code from a GitHub repository
                git credentialsId: 'github', url: 'git@github.com:1NAVNEETKUMAR1/jenkins_test.git'
				}
			}
	    stage ('print stage') {
		    steps {
			    sh 'echo "new stage"'
		    }
        stage('Build') {
            steps {
               // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit stdioRetention: '', testResults: 'api-gateway/target/surefire-reports/*.xml'
                    archiveArtifacts artifacts: 'api-gateway/target/*.jar', followSymlinks: false
                }
            }
        }
    }
}
