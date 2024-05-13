pipeline {
    agent any

    parameters {
        string defaultValue: 'us-east-1', description: 'AWS Region', name: 'aws_region'
        string defaultValue: '', description: 'Databricks Account ID', name: 'dbx_acc_id'

        string defaultValue: 'databricks-development-ws-bkt', description: 'Databricks Workspace Bucket Name', name: 'bkt_nm'
        string defaultValue: 'databricks-development-strg-config-iam-role', description: 'Databricks storage config iam role Name', name: 'strg_role_nm'
        string defaultValue: 'databricks-development-cred-config-iam-role', description: 'Databricks cred config iam role Name', name: 'cred_role_nm'
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
        stage('Workspace Bukcet Provisioning') {
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
        stage('Worspace storage config iam Provisioning') {
            steps {
                script {
                    def cloudFormationTemplate = 'workspace/workspace-strg-config-iam-role.yml'
                    def command = "aws cloudformation deploy --template-file ${cloudFormationTemplate}"
                    command += " --region ${params.aws_region}"
                    command += " --stack-name ${params.strg_role_nm}-cf-stack"
                    command += " --parameter-overrides"
                    // Add parameter values
                    command += " IamRoleName=${params.strg_role_nm}"
                    command += " DatabricksAccountIDParam=${params.dbx_acc_id}"
                    // Execute the command
                    // def command = "aws s3 ls --region ${params.aws_region}"
                    sh(command)
                }
            }
        }
        stage('Worspace cred config iam Provisioning') {
            steps {
                script {
                    def cloudFormationTemplate = 'workspace/workspace-cred-config-iam-role.yml'
                    def command = "aws cloudformation deploy --template-file ${cloudFormationTemplate}"
                    command += " --region ${params.aws_region}"
                    command += " --stack-name ${params.cred_role_nm}-cf-stack"
                    command += " --parameter-overrides"
                    // Add parameter values
                    command += " IamRoleName=${params.cred_role_nm}"
                    command += " DatabricksAccountIDParam=${params.dbx_acc_id}"
                    // Execute the command
                    // def command = "aws s3 ls --region ${params.aws_region}"
                    sh(command)
                }
            }
        }
    }
}