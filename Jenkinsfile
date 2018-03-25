pipeline {
	agent {
	 label "dynamic"
	} 
	stages {
		stage("Compile"){
			steps{
				sh "./gradlew compileJava"
			}
		}
		stage("Unit test"){
			steps{
				sh "./gradlew test"
			}
		}
		stage("Code coverage"){
			steps{
				sh "./gradlew jacocoTestReport"
				publishHTML ( target: [ 
					reportDir: 'build/reports/jacoco/test/html',
					reportFiles: 'index.html',
					reportName: 'JacoCo Report'
				])
				sh "./gradlew jacocoTestCoverageVerification"
			}
		}
		
      }
	post {
		always{
			mail to: 'traiano@gmail.com',
			subject: "Completed pipeline: ${currentBuild.fullDisplayName}",
			body: "Your build completed. Check: ${env.BUILD_URL}" 
		}
	}
}
