pipeline {
     agent {
        label 'build'
    }
    // triggers {
    //     pollSCM('*/2 * * * *') 
    // }
    
    stages {
    stage('Build') {
        steps {
            // Copy artifacts from another project
            script {
                  // Define the parameters
                    def project_name = 'package'
                    def artifact_to_copy = '**/*.war'
                    
                    // Copy artifacts from another project
                    copyArtifacts projectName: project_name, 
                                  filter: artifact_to_copy, 
                                  flatten: true
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
                tomcatUrl: 'http://54.91.14.25:8090'
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


    

