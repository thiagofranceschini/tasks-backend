pipeline {
    agent any
    stages {
        stage('Build Backend') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL')
                sh "{$scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=c1e139c794512cdbf3fee36d5bab7943c0009e57 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn**, **src/test/**, **/model/**,**Application.java"
            }
        }
    }
}

