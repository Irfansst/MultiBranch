// 👇 This goes at the very top
properties([
    parameters([
        choice(name: 'PROJECT_TO_BUILD', choices: ['All', 'Project1', 'Project2', 'Project3', 'Project4', 'Project5'], description: 'Select the project to build')
    ])
])

pipeline {
    agent any
    tools {
        maven 'Maven_3.3.9'
        jdk 'jdk-11.0.2'
    }
    stages {
        stage('Initialize Tools') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "JAVA_HOME = ${JAVA_HOME}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Build Selected Project') {
            steps {
                script {
                    def projects = ['Project1', 'Project2', 'Project3', 'Project4', 'Project5']
                    if (params.PROJECT_TO_BUILD == 'All') {
                        for (project in projects) {
                            echo "Building ${project}"
                            dir(project) {
                                sh 'mvn clean install'
                            }
                        }
                    } else {
                        echo "Building ${params.PROJECT_TO_BUILD}"
                        dir(params.PROJECT_TO_BUILD) {
                            sh 'mvn clean install'
                        }
                    }
                }
            }
        }
        stage('Archive JARs') {
            steps {
                script {
                    def projects = (params.PROJECT_TO_BUILD == 'All') ? ['Project1', 'Project2', 'Project3', 'Project4', 'Project5'] : [params.PROJECT_TO_BUILD]
                    for (project in projects) {
                        archiveArtifacts artifacts: "${project}/target/*.jar", allowEmptyArchive: true
                    }
                }
            }
        }
    }
}
