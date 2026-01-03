pipeline {
  agent any 

  stages {
    stage('Daily Compliance Run') {
      steps{
        echo 'Running a compliance scan with inspec....'
          script{
            def remote = [:]
            remote.name = "controlnode"
            remote.host = "192.168.1.12"
            remote.allowAnyHosts = true

            withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {


               def remote = [:]
                        remote.name = "controlnode"
                        remote.host = "192.168.1.12"
                        remote.allowAnyHosts = true
                        remote.user = userName
                        remote.identityFile = identity
                        
                        stage("Placeholder Stage...") {
                            // Используем sshCommand шаг правильно
                            sshCommand remote: remote, command: 'ls -l'
                            
                            // Для выполнения с sudo:
                            // sshCommand remote: remote, sudo: true, command: 'ls -l'
                        }

              
              //   remote.user = userName
              //   remote.identityFile = identity
              //   stage("Placeholder Stage...") {
              //     // sshCommand remote: remote, sudo: true, command: 'echo "add your stuff here....."'
              //     // sshCommand remote: remote, sudo: true, command: 'echo "some more stuff goes here....."'

              //     remote(remote) { channel ->
              //         // Use 'channel' to access methods/properties
              //         channel.sshCommand(command: "ls -l") 
              //     }
              // }
              //   stage("Scan with InSpec") {
              //     sshCommand remote: remote, sudo: true, command: 'inspec exec /root/linux-baseline/'
              // }
            }
          }
       }
    }
  }
}
