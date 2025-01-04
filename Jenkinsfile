@Library('my-shared-library@main') _

pipeline {
    agent { label 'dev' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
		scripts {
                pipeline1.check_out()
			}
            }
        }

        stage('Set up Java 17') {
            steps {
                scripts {
                pipeline1.setup_java()
			}
            }
        }

        stage('Set up Maven') {
            steps {
                scripts {
                pipeline1.setup_maven()
			}
            }
        }

        stage('Build with Maven') {
            steps {
                scripts {
                pipeline1.setup_build()
			}
            }
        }

        stage('Upload Artifact') {
            steps {
                echo 'Uploading artifact...'
                pipeline1.upload_artifact(String artifactPath)
            }
        }

        stage('Run Application') {
            steps {
                scripts {
                pipeline1.run_application()
			}
            }
        }

        stage('Validate App is Running') {
            steps {
                scripts {
                pipeline1.validate_app()
			}
            }
        }
		
		stage('Keeping application up for 2 mins') {
            steps {
				scripts {
                pipeline1.keep_app()
			}
            }
        }

        stage('Gracefully Stop Spring Boot App') {
            steps {
                scripts {
                pipeline1.stop_app()
			}
            }
        }
    }

    post {
        always {
            pipeline1.clean_app()
        }
    }
}
