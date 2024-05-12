// Filename: Jenkinsfile
node {

    def GITREPOREMOTE = "https://github.com/biswarup-nandi/jenkins-cloudformation.git"
    def GITBRANCH     = "main"
    def AWSCLIPATH     = "/usr/bin"

    // parameters {
    //     string defaultValue: 'databricks-development-ws-bkt', description: 'Databricks Workspace Bucket Name', name: 'bkt_nm'
    //     string defaultValue: '', description: 'Databricks Account ID', name: 'dbx_acc_id'
    // }

    stage('Checkout') {
        git branch: GITBRANCH, url: GITREPOREMOTE
    }

    // stage('Deploy Workspace Bucket CF Template') {
    //     steps {
    //         script {
    //             def cloudFormationTemplate = 'workspace/workspace-bkt.yml'
    //             def command = "aws cloudformation deploy --template-file ${cloudFormationTemplate}"
    //             command += " --parameter-overrides"
    //             // Add parameter values
    //             command += " BucketNameParam=${params.bkt_nm}"
    //             command += " DatabricksAccountIDParam=${params.dbx_acc_id}"
    //             // Execute the command
    //             sh(command)
    //         }
    //     }
    // }
}