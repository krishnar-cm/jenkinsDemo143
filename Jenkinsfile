pipeline {
    agent any
    stages {
        stage('Discover Jenkinsfiles') {
            steps {
                script {
                    // List all Jenkinsfiles in the repository
                    def jenkinsFiles = sh(script: 'git ls-files | grep Jenkinsfile', returnStdout: true).trim().split('\n')
                    echo "All Jenkinsfile: ${jenkinsFiles}"
                    // Create a job for each Jenkinsfile found
                    jenkinsFiles.each { jfile ->
                        echo "Found Jenkinsfile: ${jfile}"
                        build job: "${env.JOB_NAME}/${jfile}", wait: false // Trigger separate jobs for each Jenkinsfile
                    }
                }
            }
        }
    }
}
