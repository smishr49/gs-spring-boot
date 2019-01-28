node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      
      def mvn_version = 'Maven'
   
      withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
      sh '''
      whoami
      //usermod -a -G sudo jenkins
      //chmod +x /var/lib/jenkins/workspace/AzureDeployment_Demo
    // Run the maven build
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp todo-app-java-on-azure-1.0-SNAPSHOT.jar app.jar 
         zip todo.zip app.jar web.config
      '''
   }
      
      
     
          
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}
