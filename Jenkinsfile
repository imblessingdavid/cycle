pipeline {
    agent any
    tools{
        // maven version
       maven 'mymaven'
    }
    stages{
     stage('clonerepo')
     {
         steps{
             git branch: 'main', url: 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
       }
     }
     stage('compile')
     {
         steps{
             sh 'mvn compile'
         }
     }
     stage('codereview')
     {
         steps{
             sh 'pmd:pmd'
         }
         post{
             success{
                 recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
             }
         }
     }
     stage(test)
     {
         steps{
             sh 'mvn test'
         }
         post{
             success{
                 junit '**/target/surefire-reports/*.xml'
             }
         }
     }
     stage("package")
     {
         steps{
             sh 'mvn package'
         }
     }
    }
}
