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
    
    mail bcc: '', body: 'job run', cc: '', from: '', replyTo: '', subject: 'jenkins notification', to: 'aalapkotekar@gmail.com'

    
}
