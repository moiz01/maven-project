pipeline {
    agent {
        label 'build'
    }
     //environment {
          
        // M2_HOME = tool 'localMAVEN-3.8.8'
	   //   DOTNET_ROOT = "/usr/bin/dotnet"
   // }



    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Check Version'){

            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

    }
}