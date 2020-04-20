pipeline{
    tools{
        jdk 'awsjava'
        maven 'awsmaven'
    }
    agent any
    stages{
        stage('Checkout'){
            steps{
               git 'https://github.com/venkatgit7/devops.git'  
            }
           
        }
        stage('Compile'){
            steps {
            sh 'mvn compile'
            }
        }
         stage('CodeReview'){
            steps {
            sh 'mvn pmd:pmd'
            }
			post{
				always{
					pmd pattern: 'target/pmd.xml'
				}
			}
        }
         stage('UnitTest'){
            steps {
            sh 'mvn test'
            }
			post {
				always{
				junit testResults: 'target/surefire-reports/*.xml'
				}
			}
        }
        stage('MetricCheck'){
            steps{
            sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
			post {
				always {
					cobertura coberturaReportFile : 'target/site/cobertura/coverage.xml'
				}
			}
        }
        stage('Package'){
            steps{
            sh 'mvn package'
            }
        }
    }
}