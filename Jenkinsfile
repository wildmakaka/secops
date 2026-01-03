pipeline {
  agent any 

  stages {
    stage('Compliance Scan') {
      steps {
        script {
          // Используем withCredentials для получения данных
          withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', 
                                           keyFileVariable: 'identity', 
                                           usernameVariable: 'userName')]) {
            
            // Определяем remote как Map (это решает проблему с MissingPropertyException)
            def remote = [
              name: "controlnode",
              host: "192.168.1.12",
              user: userName,
              identityFile: identity,
              allowAnyHosts: true
            ]

            echo "--- Подготовка к сканированию ---"
            sshCommand remote: remote, sudo: true, command: 'echo "Checking connection..." && uptime'

            echo "--- Запуск InSpec ---"
            // Используем failOnError: false, чтобы пайплайн не падал при обнаружении уязвимостей
            sshCommand remote: remote, sudo: true, command: 'inspec exec /root/linux-baseline/'
          }
        }
      }
    }
  }
}
