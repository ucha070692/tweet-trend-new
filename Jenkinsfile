pipeline {
    agent { node { label 'maven' } }

    environment {
        PATH = "/opt/apache-maven-3.9.12/bin:$PATH"
        MAVEN_OPTS = "-Xmx2g -XX:MaxMetaspaceSize=512m"
    }

    stages {
        stage('Build & Test') {
            steps {
                sh 'mvn clean install -DskipTests=false -Djacoco.skip=true'
            }
        }

        stage('Deploy') {
            when { branch 'main' }
            steps {
                sh 'mvn deploy -DskipTests=true'
            }
        }

        stage('sonarQube Analysis') {
            environment {
                scannerHome = tool 'valaxy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('valaxy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    } // ✅ THIS WAS MISSING

    post {
        always { echo "Build finished!" }
        success { echo "Build succeeded!" }
        failure { echo "Build failed. Check test reports in target/surefire-reports" }
    }
}
