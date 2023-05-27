pipeline {
  agent {label 'slave01' }
  
  stages{
   stage('Checkout SCM') {
     steps {
       checkout scm
     }
    }
  
   stage('Deploy ansible playbook') {
     steps {
        sh """
           echo "Checking if remote node can be reached..."
           ansible web -m ping

           echo "Deploying ansible playbook..."
           ansible-playbook devplay.yml --check

           """
       }
    }

   stage('Approve to deploy play') {
       options{
         timeout(time: 1, unit: 'MINUTES')
          }
       steps{
         input "Approve to run the playbook"
         sh """
 
           echo "Deploying ansible playbook..."
           ansible-playbook devplay.yml 

           """
         }
       }
    }
}

           
