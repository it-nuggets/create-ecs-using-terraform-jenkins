pipeline{
    agent any
    tools {
        terraform 'terraform'
    }

    parameters {
        choice(name: 'TERRAFORM_OPERATION', choices: ['plan', 'apply', 'destroy'], description: 'Select Terraform Operation')
    }

    stages{
        stage('checkout from GIT'){
            steps{
                git branch: 'main', url: 'https://github.com/it-nuggets/create-ecs-using-terraform-jenkins.git'
            }
        }
        stage('Terraform init'){
            steps{
                
                sh 'terraform init'
            }
        }
        stage('Terraform Operation') {
            steps {
                script {
                    // Run Terraform based on the selected operation
                    switch(params.TERRAFORM_OPERATION) {
                        case 'plan':
                            sh "terraform plan"
                            break
                        case 'apply':
                            sh 'terraform apply -auto-approve'
                            break
                        case 'destroy':
                            sh "terraform destroy -auto-approve"
                            break
                        default:
                            error "Invalid Terraform operation selected"
                    }
                }
            }
        }
    }

}