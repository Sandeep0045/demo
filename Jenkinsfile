 pipeline {

  agent any
  environment {
     TF_VAR_okta_group_name=var.okta_group_name
}

  parameters {
      string(name: 'okta_group_name', defaultValue: 'xxx', )

  }
  stages {

    stage('TF Plan') {
      steps {
          sh 'terraform init'
          sh 'terraform plan -out myplan'
        }
      }


    stage('Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }

    stage('TF Apply') {
      steps {
          sh 'terraform apply -input=false myplan'
        }
      }
  }

}
