pipeline {
    agent  any
    stages {
        stage('deployments') {
            parallel {
                stage('deploy to stg') {
                    steps {
                        echo 'stg deployment done'
                    }
                }
                stage('deploy to prod') {
                    steps {
                        echo 'prod deployment done'
                    }
                }
                 stage('Invoke GitHub Actions Workflow') {
                    steps {
                        script {
                            try {
                                def url = "https://api.github.com/repos/rachellerathbone/new-repo-new-change/actions/workflows/build.yml/dispatches"
                                def response = sh(script: 'curl -X POST -H "Accept: application/vnd.github.v3+json" -H "authorization: Bearer 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" -d \'{"ref":"TEST-392-build"}\' "${url}"', returnStdout: true).trim()
                                echo "Response: ${response}"
                            } catch (Exception e) {
                                echo "Failed to invoke GitHub Actions Workflow: ${e.getMessage()}"
                                currentBuild.result = 'FAILURE'
                            }
                        }
                    }
                }
            }
           post {
                 always {
                     jiraSendDeploymentInfo site: 'rachellerathbone.atlassian.net'
                 }
             }
        }
        stage('build') {
             steps {
                echo 'Building..'
             }
             post {
                 always {
                     jiraSendBuildInfo site: 'rachellerathbone.atlassian.net'
                 }
             }
         }
    }
}
