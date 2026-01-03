pipeline {
    agent any
    stages {
        stage('Compliance Scan') {
            steps {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', 
                                                     keyFileVariable: 'identity', 
                                                     usernameVariable: 'userName')]) {
                        
                        // Прямая передача параметров в блок с использованием pty: true
                        // pty: true критичен для последних версий Linux при использовании sudo
                        withSSH(remote: [host: '192.168.1.12', 
                                       user: userName, 
                                       identityFile: identity, 
                                       allowAnyHosts: true,
                                       pty: true]) {
                            
                            echo "--- Running Scan ---"
                            sshCommand sudo: true, command: 'inspec exec /root/linux-baseline/'
                        }
                    }
                }
            }
        }
    }
}
