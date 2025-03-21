pipeline {
    agent any
    stages {
        stage('Discover and Execute Pipelines') {
            steps {
                script {
                    def files = sh(script: 'git ls-files | grep Jenkinsfile', returnStdout: true).trim().split('\n')
                    for (file in files) {
                        echo "Executing pipeline: ${file}"
                        load file
                    }
                }
            }
        }
    }
}
