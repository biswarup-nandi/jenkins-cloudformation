// Filename: Jenkinsfile
node {
    agent all

    def GITREPOREMOTE = "https://github.com/biswarup-nandi/jenkins-cloudformation.git"
    def GITBRANCH     = "main"
    def AWSCLIPATH     = "/usr/bin"

    parameters {
        string(name: 'WS_BKT', defaultValue: 'databricks-development-ws-bkt', description: 'Enter Workspace Bucket Name')
        string(name: 'WS_STRG_CONFG_IAM_ROLE', defaultValue: 'ws-strg-config-iam-role.yml', description: 'Enter IAM Role Name for Storage Config')
        string(name: 'WS_CRED_CONFG_IAM_ROLE', defaultValue: 'ws-cred-config-iam-role.yml', description: 'Enter IAM Role Name for Credential Config')
    }

    stage('Checkout') {
        git branch: GITBRANCH, url: GITREPOREMOTE
    }

    stage('Validation') {
        sh """#!/bin/bash
            ls
            aws s3 ls
            echo $WS_STRG_CONFG_IAM_ROLE
        """
    }
}