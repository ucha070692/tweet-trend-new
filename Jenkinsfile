pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('Clone code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ucha070692/tweet-trend-new.git'
            }
        }
    }
}

