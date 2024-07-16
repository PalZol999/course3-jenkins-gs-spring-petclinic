pipeline {
    agent any
    
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PalZol999/course3-jenkins-gs-spring-petclinic'
            }
        }
        
        stage('build') {
            steps {
                sh './mvnw clean package'
            }
        }
        
        stage('capture') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar'
                junit '**/target/surefire-reports/TEST-*.xml'
                jacoco()
            }
        }
        
        stage('parallel tests') {
            parallel {
                stage('testA') {
                    steps {
                        sh "echo test set A"
                        sleep 2
                        sleep 3
                    }
                }
                stage('testB') {
                    steps {
                        sh "echo test set B"
                        sleep 4
                    }
                }
            }
        }
    }
       
    post {
        always {
            echo "Performing cleanup tasks"
        }
    }
}
