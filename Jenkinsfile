// Job_Name = IssueName
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh "echo build"
            }
        }
    }
    
    post {
        success {
            script {
                def transitionInput =
                [
                    transition: [
                        id: '41'
                    ]
                ]
                jiraTransitionIssue idOrKey: "${env.JOB_NAME}", input: transitionInput, site: 'jira'
            }
        }
    }
}
