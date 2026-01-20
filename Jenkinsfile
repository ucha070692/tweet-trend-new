pipeline {
    agent { node { label 'maven' } }

    environment {
        PATH = "/opt/apache-maven-3.9.12/bin:$PATH"
        MAVEN_OPTS = "-Xmx2g -XX:MaxMetaspaceSize=512m"
    }

    stages {
        stage('Build & Test') {
            steps {
                // Skip tests if Surefire keeps crashing
                sh 'mvn clean install -DskipTests=false -Djacoco.skip=true'
            }
        }

        stage('Deploy') {
            when { branch 'main' }
            steps {
                sh 'mvn deploy -DskipTests=true'
            }
        }
    }

    post {
        always { echo "Build finished!" }
        success { echo "Build succeeded!" }
        failure { echo "Build failed. Check test reports in target/surefire-reports" }
    }
}
