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
             copyArtifacts(projectName: 'package');

            script {
             // Define the upstream project name
                    def upstreamProject = 'package'
                    // Define the artifact file name pattern
                    def artifactPattern = '**/*.war'

                    // Copy the artifact from the upstream project
                    copyArtifacts(
                        projectName: upstreamProject,
                        filter: artifactPattern
                    )
            //       // Define the parameters
            //         def project_name = 'package'
            //         def artifactDir = 'webapp/target'
            //         def artifactPattern = '*.war'
            //         def artifact_to_copy = '**/target/*.war'
                    
            //         // Copy artifacts from another project
            //         copyArtifacts projectName: project_name, 
            //                        filter: artifactPattern,
            //                       target: artifactDir
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


    

