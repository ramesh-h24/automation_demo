pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '${sha1}']], extensions: [], userRemoteConfigs: [[credentialsId: 'Git', refspec: '+refs/pull/*:refs/remotes/origin/pr/*', url: 'https://github.com/ramesh-h24/automation_demo.git']])

        stage('Pull PR Branches') {
            steps {
                checkout scmGit(branches: [[name: '${sha1}']], extensions: [], userRemoteConfigs: [[credentialsId: 'Git', refspec: '+refs/pull/*:refs/remotes/origin/pr/*', url: 'https://github.com/ramesh-h24/automation_demo.git']])
                sh 'git fetch origin +refs/pull/*:refs/remotes/origin/pr/*' // Fetch PR branches
                sh 'git checkout ${env.BRANCH_NAME}' // Switch to the current branch
                sh 'git pull origin ${env.BRANCH_NAME}' // Pull latest changes
            }
        }


        stage('Check Merging') {
            steps {
                script {
                     if (env.BRANCH_NAME == 'main') {
                     sh 'git checkout main'
                     sh 'git merge --no-ff ${env.BRANCH_NAME}'
                   // Add conflict resolution steps if needed
                     } else if (env.BRANCH_NAME.startsWith('feature')) {
                     echo 'PR occurs'
                    // Additional steps for handling PRs
                     } else {
                     echo "Skipping this stage for other branches."
                     }
               }
            }
       }

    }
}
