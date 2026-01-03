groovy
pipeline {
    agent any 

    stages {
        stage('Daily Compliance Run') {
            steps {
                script {
                    // Настройка подключения
                    def remote = [:]
                    remote.name = "controlnode"
                    remote.host = "192.168.1.12"
                    remote.allowAnyHosts = true

                    withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', 
                                                     keyFileVariable: 'identity', 
                                                     passphraseVariable: '', 
                                                     usernameVariable: 'userName')]) {
                        
                        remote.user = userName
                        remote.identityFile = identity

                        // Вместо вложенных stage используем логические блоки или echo
                        echo "--- Starting Configuration Phase ---"
                        sshCommand remote: remote, sudo: true, command: 'echo "Running setup commands..."'
                        sshCommand remote: remote, sudo: true, command: 'uptime'

                        echo "--- Starting InSpec Scan ---"
                        // failOnError: false позволит пайплайну завершиться и сформировать отчет, 
                        // даже если проверки InSpec не пройдены
                        sshCommand remote: remote, sudo: true, command: 'inspec exec /root/linux-baseline/'
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo "Compliance run finished."
        }
    }
}
