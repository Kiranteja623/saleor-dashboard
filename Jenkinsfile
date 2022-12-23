pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'dev', url: 'https://github.com/Kiranteja623/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                sh 'sudo docker image build -t kiranteja623/salesdashboard .'
                //sh 'docker image build -t shaikkhajaibrahim/saleor-dashboar:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                  sh 'sudo docker image push kiranteja623/salesdashboard'
                //sh 'docker image push shaikkhajaibrahim/saleor-dashboar:DEV'
            }
        }
        stage('create terraform') {
            steps {
                  git url: 'git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster'
                  sh 'terraform init && terraform apply -auto-approve'
                  sh 'aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)'
                //sh 'docker image push shaikkhajaibrahim/saleor-dashboar:DEV'
            }
    }
}

