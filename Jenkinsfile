pipeline {
     agent {
        label 'build'
    }
    // triggers {
    //     pollSCM('*/2 * * * *') 
    // }
    
    stages {
         stage('Copy Archive') {
         steps {
             script {
                step ([$class: 'CopyArtifact',
                    projectName: 'package',
                    filter: "webapp/target/*.war",
                    target: 'Infra']);
            }
        }
    }
    
        
 

        
       
    }

 
    
    // post {
    //     always {
    //         // Deploy WAR/EAR to Tomcat
    //         deployWarToTomcat(
    //             warFiles: '**/*.war',
    //             managerUser: 'admin',
    //             managerPassword: 'rp@P8on!',
    //             tomcatUrl: 'http://34.236.242.150:8090'
    //         )
    //     }
    // }
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


    

