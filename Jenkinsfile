/* pipeline {
	agent any
	stages {
		stage ('build') {
			echo ''
		}
		stage ('test: integration-&-quality') {
			...
		}
		stage ('test: functional') {
			...
		}
		stage ('test: load-&-security') {
			...
		}
		stage ('approval') {
			...
		}
		stage ('deploy:prod') {
			...
		}
	} */

pipeline {
    agent any

    environment {
        DONT_COLLECT = 'FOO'
    }

    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/guthakondalu/jenkins-git-integration.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                echo "Artifactory configuration"
                }
        }

        stage ('Config Build Info') {
             steps {
                echo "mvn clean install"
                }
        }

        stage ('Exec Gradle') {
             steps {
                echo "Exec Gradle"
                }
        }

        stage ('Publish build info') {
             steps {
                echo "Publish Build Info"
                }
        }
    }
}