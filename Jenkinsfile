pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample-multibranch/umaima', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
            withCredentials([sshUserPrivateKey(credentialsId: "vagrant-private-key", keyFileVariable: 'keyfile')]) {
            sh 'scp -i ${keyfile} ./sample vagrant@10.10.50.3:'
        }
      }
    }

  }
}
