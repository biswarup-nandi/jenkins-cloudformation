pipeline {
    agent any

    stages {
        stage('Validating Files') {
            steps {
                sh("ls -ltr")
                sh("cd workspace")
                sh("ls -ltr")
            }
        }
        // stage('Test') {
        //     steps {
        //         echo 'Testing..'
        //     }
        // }
        // stage('Deploy') {
        //     steps {
        //         echo 'Deploying....'
        //     }
        // }
    }
}

// // Filename: Jenkinsfile
// node {

//     agent any

//     // def GITREPOREMOTE = "https://github.com/biswarup-nandi/jenkins-cloudformation.git"
//     // def GITBRANCH     = "main"
//     // def AWSCLIPATH     = "/usr/bin"

//     parameters {
//         string defaultValue: 'databricks-development-ws-bkt', description: 'Databricks Workspace Bucket Name', name: 'bkt_nm'
//         string defaultValue: '', description: 'Databricks Account ID', name: 'dbx_acc_id'
//     }

//     stages {
//         stage('Checkout') {
//             // git branch: GITBRANCH, url: GITREPOREMOTE
//             steps {
//                 echo "Bucket Name ${params.bkt_nm}"
//             }
//         }

//         // stage('Deploy Workspace Bucket CF Template') {
//         //     sh """
//         //         #!/bin/bash
//         //         echo "Bucket Name: ${params.bkt_nm}"
//         //     """
//         //     // steps {
//         //     //     script {
//         //     //         // def cloudFormationTemplate = 'workspace/workspace-bkt.yml'
//         //     //         // def command = "aws cloudformation deploy --template-file ${cloudFormationTemplate}"
//         //     //         // command += " --parameter-overrides"
//         //     //         // // Add parameter values
//         //     //         // command += " BucketNameParam=${params.bkt_nm}"
//         //     //         // command += " DatabricksAccountIDParam=${params.dbx_acc_id}"
//         //     //         // // Execute the command
//         //     //         def command = "echo ${params.bkt_nm}"
//         //     //         sh(command)
//         //     //     }
//         //     // }
//         // }
//     }
    
// }