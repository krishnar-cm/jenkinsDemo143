
pipeline {
    agent any
    stages {
        stage('Discover Jenkinsfiles') {
steps {
def jenkinsFiles = sh(script: 'git ls-files --exclude-standard -- ":!:Jenkinsfile" | grep Jenkinsfile', returnStdout: true).trim().split('\n')
     echo "All Jenkinsfile: ${jenkinsFiles}"
    jenkinsFiles.each { jenkinsFile ->
    def jobName = jenkinsFile.replace('/', '_').replace('Jenkinsfile', '').trim()
    if (Jenkins.instance.getItem(jobName) == null) {
        println "Creating pipeline job: ${jobName}"
        def pipelineJob = Jenkins.instance.createProject(org.jenkinsci.plugins.workflow.job.WorkflowJob, jobName)
        pipelineJob.definition = new org.jenkinsci.plugins.workflow.cps.CpsScmFlowDefinition(
            new hudson.plugins.git.GitSCM(repoUrl),
            jenkinsFile
        )
        pipelineJob.save()
    } else {
        println "Pipeline job ${jobName} already exists."
    }
}
}
        }
    }
}

// pipeline {
//     agent any
//     stages {
//         stage('Discover Jenkinsfiles') {
//             steps {
//                 script {
//                     // List all Jenkinsfiles in the repository
//                     def jenkinsFiles = sh(script: 'git ls-files | grep Jenkinsfile', returnStdout: true).trim().split('\n')
//                     echo "All Jenkinsfile: ${jenkinsFiles}"
//                     // Create a job for each Jenkinsfile found
//                     jenkinsFiles.each { jfile ->
//                         echo "Found Jenkinsfile: ${jfile}"
//                         build job: "${env.JOB_NAME}/${jfile}", wait: false // Trigger separate jobs for each Jenkinsfile
//                     }
//                 }
//             }
//         }
//     }
// }
