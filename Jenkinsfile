pipeline {
    agent any
    tools {
        maven 'M3'
    }
    stages {
        stage('Build') {
            steps {
                dir ('TDD-Java-Course'){
                    sh 'mvn clean compile'
                }
            }
        }
        stage('Db') {
            steps {
                dir ('liquibase'){
                    sh '/usr/local/bin/liquibase/liquibase --changeLogFile="changesets/db.changelog-master.xml" update'
                }
            }
        }
        stage('Sonar') {
            steps {
                dir ('TDD-Java-Course'){
                    sh 'mvn test jacoco:report'
                    sh 'mvn sonar:sonar \
                        -Dsonar.projectKey=TDD-Java_sonar \
                        -Dsonar.projectName=TDD-Java_sonar \
                        -Dsonar.sources=src/main \
                        -Dsonar.host.url=http://192.168.15.15:9000 \
                        -Dsonar.login=0d941f3fe87a11d4842c8a2a138e876791684aa7'
                }
            }
        }
    }
}