pipeline {
     agent {
        label 'build'
    }
    triggers {
        pollSCM('*/2 * * * *') 
    }
    
    stages {
     stage('Build war'){
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
    
    post {
        always {
            // Deploy WAR/EAR to Tomcat
            deployWarToTomcat(
                warFiles: '**/*.war',
                managerUser: 'admin',
                managerPassword: 'rp@P8on!',
                tomcatUrl: 'http://18.234.220.117:8090'
            )
        }
    }
}

def deployWarToTomcat(Map params) {
    // Retrieve parameters
    def warFiles = params.warFiles
    def managerUser = params.managerUser
    def managerPassword = params.managerPassword
    def tomcatUrl = params.tomcatUrl
    

    
    // Deploy WAR/EAR to Tomcat using the Deploy plugin
    echo "Deploying WAR files to Tomcat..."
          deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', url: tomcatUrl, path: '/manager/text')], contextPath: '', war: warFiles

}


    

