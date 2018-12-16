node {
  stage('init') {
    checkout scm
  }

  stage('build') {
    sh 'mvn clean package'
  }

  stage('deploy') {
    def resourceGroup = env.RES_GROUP
    def webAppName = env.WEB_APP
    sh 'mv target/*.war target/ROOT.war'
    azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID, publishType: 'file',
                       resourceGroup: env.RES_GROUP, appName: env.WEB_APP,
                       filePath: '*.war', sourceDirectory: 'target', targetDirectory: 'webapps'
  }
}
