pipeline {
  agent any 

  stages {
    stage('Daily Compliance Run') {
      steps {
        script {
          withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', 
                                           keyFileVariable: 'identity', 
                                           usernameVariable: 'userName')]) {
            
            // РЕШЕНИЕ: Создаем объект remote сразу целиком как Map
            def remote = [
              name: "controlnode",
              host: "192.168.1.12",
              user: userName,
              identityFile: identity,
              allowAnyHosts: true
            ]

            echo "--- Configuration Phase ---"
            sshCommand remote: remote, sudo: true, command: 'uptime'

            echo "--- InSpec Scan ---"
            // failOnError: false позволит продолжить, если InSpec найдет уязвимости
            sshCommand remote: remote, sudo: true, command: 'inspec exec /root/linux-baseline/', failOnError: false
          }
        }
      }
    }
  }
}
