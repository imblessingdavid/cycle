pipeline{
    
    tools{
        // what tool version to use for build stages
        maven 'mymaven'
    }
    
    agent any
    
    stages{
        
        stage ('CloneRepo')
        {
            steps{
             echo 'This is stage 1'
              git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'  
            }
        }
        
        stage ('Compile')
        {
            steps{
                
             sh  'mvn compile'
                
            }
        }
        stage ('CodeReview')
        {
            steps{
                
             sh  'mvn pmd:pmd'
                
            }
            post{
                success{
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
            }
        }
        stage ('Test')
        {
            steps{
                
             sh  'mvn test'
                
            }
        post{
            success{
                junit 'target/surefire-reports/*.xml'
            }
        }
        }
        
        stage('package')
        {
            steps{
                sh 'mvn package'
            }
        }
        
    }
    
    
    
}
