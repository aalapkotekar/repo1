node 
{
	stage ('git checkout') {
checkout([$class: 'GitSCM', 
branches: [[name: '*/master']],
doGenerateSubmoduleConfigurations: false, 
extensions: [], submoduleCfg: [],
userRemoteConfigs: [[url: 'https://github.com/aalapkotekar/repo1.git']]])
							}
   
    stage ('app build')
    {
   	sh 'mvn clean package'
    }

    stage  ('Archive')
    {
        archiveArtifacts 'target/Helloworldwebapp.war'

    }

    input 'Deploy to Prod Server?'

    stage ('deploy')
    {
    	sh 'cp target/Helloworldwebapp.war /opt/tomcat/webapps/'
    }
    
	notify('Deploy done')
    
}

def notify(status) {
  mail (
        body:"""${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
                 Check console output at, 
                 href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]""",
        cc: '', 
        subject: """JenkinsNotification: ${status}:""", 
        to: 'aalapkotekar@gmail.com'  
       ) 
 }
