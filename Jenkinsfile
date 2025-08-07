pipeline {
    agent any
	tools { 
        maven 'Maven_3.3.9' 
        jdk 'jdk-11.0.2' 
    }	
    stages {
	
		stage ('Tools Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
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
