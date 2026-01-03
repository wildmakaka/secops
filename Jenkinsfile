pipeline {
  agent any 

  stages {
    stage('Daily Compliance Run') {
      steps {
        echo 'Running a compliance scan with inspec....'
        script {
          def remote = [:]
          remote.name = "controlnode"
          remote.host = "192.168.1.12"
          remote.user = "marley"  // или ваш пользователь
          remote.allowAnyHosts = true

          withCredentials([sshUserPrivateKey(
            credentialsId: 'sshUser', 
            keyFileVariable: 'identity', 
            passphraseVariable: '', 
            usernameVariable: 'userName'
          )]) {
            remote.user = userName
            remote.identityFile = identity
            
            // Инициализируем SSH сессию
            ssh.session(remote) {
              stage("Placeholder Stage...") {
                // Команда с sudo
                executeSudo('echo "add your stuff here....."')
                executeSudo('echo "some more stuff goes here....."')
              }
              
              stage("Scan with InSpec") {
                executeSudo('inspec exec /root/linux-baseline/')
              }
            }
          }
        }
      }
    }
  }
}
