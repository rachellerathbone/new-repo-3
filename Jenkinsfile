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
                stage('GitHub Jenkins Ant Docker Build') {
                  steps {
                    git 'https://github.com/rachellerathbone/new-repo-new-change.git'
                    sh 'testing jenkins with actions'
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
