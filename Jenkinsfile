pipeline {
    agent any

    parameters {
        string defaultValue: 'us-east-1', description: 'AWS Region', name: 'aws_region'
        string defaultValue: '', description: 'Databricks Account ID', name: 'dbx_acc_id'

        string defaultValue: 'databricks-development-ws-bkt', description: 'Databricks Workspace Bucket Name', name: 'bkt_nm'
    }

    stages {
        stage('CloudFormation Template Validation') {
            steps {
                script {
                    // Capture the output of the shell command
                    def commandOutput = sh(script: 'ls workspace/*.yml | wc -l', returnStdout: true).trim()
                    
                    // Convert the output to an integer
                    def result = commandOutput.toInteger()

                    if (result != 3) {
                        error("Expected 3 .yml files in workspace, but found $result")
                    } else {
                        echo "Validation successful. Moving to next stage."
                    }
                }
            }
        }
        stage('Worspace Bukcet Provisioning') {
            steps {
                script {
                    def cloudFormationTemplate = 'workspace/workspace-bkt.yml'
                    def command = "aws cloudformation deploy --template-file ${cloudFormationTemplate}"
                    command += " --region ${params.aws_region}"
                    command += " --stack-name ${params.bkt_nm}-cf-stack"
                    command += " --parameter-overrides"
                    // Add parameter values
                    command += " BucketNameParam=${params.bkt_nm}"
                    command += " DatabricksAccountIDParam=${params.dbx_acc_id}"
                    // Execute the command
                    // def command = "aws s3 ls --region ${params.aws_region}"
                    sh(command)
                }
            }
        }
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