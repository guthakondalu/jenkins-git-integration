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

    parameters { 
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0','1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
        choice(
            name: 'Env',
            choices: ['DEV', 'QA', 'UAT', 'PROD'],
            description: 'Passing the Environment'
        )
    }

    stages {
        stage ('build') {
            steps {
                git branch: 'master', url: "https://github.com/guthakondalu/jenkins-git-integration.git"
            }
        }

        stage ('test') {
            steps {
                echo "Artifactory configuration"
                }
        }

        stage ('deplpoy') {
             steps {
                    echo "Build information"
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
    post{
        always{
            echo "Build success"
        }
        failure{
            echo "Build Failed"
        }
    }
}