pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = "AKIAVIMAPNUDABOBKWGC"
        AWS_SECRET_ACCESS_KEY = "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"
        AWS_DEFAULT_REGION = "ap-south-1"
    }
    stages {
        stage("Create an EKS Cluster") {
            steps {
                script {
                    dir('part2-cluster-from-terraform-and-jenkins/terraform-for-cluster') {
                        sh "terraform init"
                        sh "terraform validate"
                        sh "terraform plan"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }
        stage("Deploy to EKS") {
            steps {
                script {
                    dir('part2-cluster-from-terraform-and-jenkins/kubernetes') {
                        sh "aws eks update-kubeconfig --name myjenkins-server-eks-cluster --region ap-south-1"
                        sh "kubectl apply -f deployment.yaml"
                        sh "kubectl apply -f service.yaml"
                    }
                }
            }
        }
    }
}