pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main'], [name: 'feature']], extensions: [], userRemoteConfigs: [[credentialsId: 'Git', url: 'https://github.com/ramesh-h24/automation_demo.git']])
            }
        }

        stage('Pull PR Branches') {
            when {
                expression { env.BRANCH_NAME.startsWith('feature') }
            }
            steps {
                // Your build steps for PR branches go here
                sh 'git pull origin feature'
            }
        }

        stage('Check Merging') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        // Handle merging into master (e.g., deploy)
                        echo 'echo test merging if no conflicts'
                    } else if (env.BRANCH_NAME.startsWith('feature')) {
                        // Handle pull request (e.g., test)
                        echo 'PR occurs'
                    } else {
                        // Handle other branches (if needed)
                        echo "Skipping this stage for non-PR branches."
                    }
                }
            }
        }
    }
}
