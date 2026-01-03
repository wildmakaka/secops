pipeline {
  agent any 

  stages {
    stage('Daily Compliance Run') {
      steps {
        echo 'Running a compliance scan with inspec....'
        script {
          withCredentials([sshUserPrivateKey(
            credentialsId: 'sshUser', 
            keyFileVariable: 'identity', 
            passphraseVariable: '', 
            usernameVariable: 'userName'
          )]) {
            
            // Определяем remote конфигурацию
            def remote = [:]
            remote.name = "controlnode"
            remote.host = "192.168.1.12"
            remote.user = userName
            remote.identityFile = identity
            remote.allowAnyHosts = true
            
            // Используем sshCommand напрямую
            stage("Placeholder Stage...") {
              sshCommand remote: remote, command: 'echo "add your stuff here....."', sudo: true
              sshCommand remote: remote, command: 'echo "some more stuff goes here....."', sudo: true
            }
            
            stage("Scan with InSpec") {
              sshCommand remote: remote, command: 'inspec exec /root/linux-baseline/', sudo: true
            }
          }
        }
      }
    }
  }
}
