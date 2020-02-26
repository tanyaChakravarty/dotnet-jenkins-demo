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
                 bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore "dotnet-jenkins-demo\\dotnet-jenkins-demo.sln" '
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
            bat "\"${tool 'msbuild'}\\MSBuild.exe\" dotnet-jenkins-demo\\jenkins-demo.sln /p:Configuration=Debug /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
      }
   }
 }
}

