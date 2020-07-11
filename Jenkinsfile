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
                rtServer (
                    id: "ARTIFACTORY_SERVER",
                    url: SERVER_URL,
                    credentialsId: CREDENTIALS
                )

                rtGradleDeployer (
                    id: "GRADLE_DEPLOYER",
                    serverId: "ARTIFACTORY_SERVER",
                    repo: "libs-snapshot-local",
                    excludePatterns: ["*.war"],
                )

                rtGradleResolver (
                    id: "GRADLE_RESOLVER",
                    serverId: "ARTIFACTORY_SERVER",
                    repo: "jcenter"
                )
            }
        }

        stage ('Config Build Info') {
            steps {
                rtBuildInfo (
                    captureEnv: true,
                    includeEnvPatterns: ["*"],
                    excludeEnvPatterns: ["DONT_COLLECT*"]
                )
            }
        }

        stage ('Exec Gradle') {
            steps {
                rtGradleRun (
                    usesPlugin: true, // Artifactory plugin already defined in build script
                    tool: GRADLE_TOOL, // Tool name from Jenkins configuration
                    rootDir: "gradle-examples/gradle-example/",
                    buildFile: 'build.gradle',
                    tasks: 'clean artifactoryPublish',
                    deployerId: "GRADLE_DEPLOYER",
                    resolverId: "GRADLE_RESOLVER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SERVER"
                )
            }
        }
    }
}