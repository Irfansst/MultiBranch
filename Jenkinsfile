pipeline {
    agent any
    stages {
        stage('Build All Projects') {
            steps {
                script {
                    def projects = ['Project1', 'Project2']
                    for (project in projects) {
                        build job: "${env.JOB_NAME}/${project}", wait: true
                    }
                }
            }
        }
    }
}
