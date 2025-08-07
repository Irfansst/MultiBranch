pipeline {
    agent any
    stages {
        stage('Build All Projects') {
            steps {
                script {
                    def projects = ['Project1', 'Project2', 'Project3', 'Project4', 'Project5']
                    for (project in projects) {
                        echo "Building ${project}"
                        dir(project) {
                            sh 'mvn clean install'
                        }
                    }
                }
            }
        }
        stage('Archive JARs') {
            steps {
                script {
                    def projects = ['Project1', 'Project2', 'Project3', 'Project4', 'Project5']
                    for (project in projects) {
                        def jarPattern = "${project}/target/*.jar"
                        archiveArtifacts artifacts: jarPattern, allowEmptyArchive: true
                    }
                }
            }
        }
    }
}
