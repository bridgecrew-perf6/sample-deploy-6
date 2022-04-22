pipeline {
  agent any
  
  parameters {
  choice choices: ['qa', 'production'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
}


  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample-multibranch/umaima', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
          sh 'ansible-playbook --private-key=${keyfile} -i ${DEPLOY_TO}.ini playbook.yml'
        }
      }
    }

  }
}
