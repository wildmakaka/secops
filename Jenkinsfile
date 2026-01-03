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


        //           remote.user = userName
        // remote.identityFile = identity
        // stage("SSH Steps Rocks!") {
        //     writeFile file: 'abc.sh', text: 'ls'
        //     sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
        //     sshPut remote: remote, from: 'abc.sh', into: '.'
        //     sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
        //     sshScript remote: remote, script: 'abc.sh'
        //     sshRemove remote: remote, path: 'abc.sh'
        // }
    

                
                
                remote.user = userName
                remote.identityFile = identity
                stage("Placeholder Stage...") {
                  sshCommand remote: remote, sudo: true, command: 'echo "add your stuff here....."'
                  sshCommand remote: remote, sudo: true, command: 'echo "some more stuff goes here....."'
              }
                stage("Scan with InSpec") {
                  sshCommand remote: remote, sudo: true, command: 'cat /etc/hosts'
              }
            }
          }
       }
    }
  }
}

