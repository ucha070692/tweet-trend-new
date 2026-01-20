pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.12/bin:$PATH"
        MAVEN_OPTS = "-Xmx2g"
    }
    
    stages {
        stage('Build & Test') {
            steps {
                // Run Maven build, skip tests if necessary
                sh 'mvn clean install -DskipTests=false'
            }
        }
        
        stage('Deploy') {
            when {
                branch 'main' // Only deploy from main branch
            }
            steps {
                sh 'mvn deploy -DskipTests=true'
            }
        }
    }
    
    post {
        always {
            echo "Build finished!"
        }
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed. Check test reports!"
        }
    }
}
