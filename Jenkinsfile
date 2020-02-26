pipeline {
agent any
 
options {
    skipDefaultCheckout()
}
environment {
   PATH = "C:\\Windows\\System32"
}
 
stages {
stage ('Checkout') {
        steps{
            checkout(scm)
            stash includes: '**', name: 'source', useDefaultExcludes: false
        }
    }
stage ('Restore Packages') {     
         steps {
             deleteDir()
             unstash 'source'
             script {
                 bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore "src\\dotnet-jenkins-demo.sln" '
             }             
          }
        }
// stage('Clean') {
//       steps {
//             bat '"C:\\Program Files\\dotnet\\dotnet.exe" clean'
//        }
//     }
stage('Build') {
     steps {
            deleteDir()
            unstash 'source'
            dir('src\\dotnet-jenkins-demo')
            script{
                bat "dotnet publish -c release -o /app --no-restore" 
            }
      }
   }
 }
}

