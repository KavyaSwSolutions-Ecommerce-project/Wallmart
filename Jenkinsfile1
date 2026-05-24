node{
    def mavenHome = tool name:"maven 3.9.15"
    stage('CheckoutCode'){
        git branch: 'main', credentialsId: 'eb2e7d91-a653-44b4-ac4d-fbd58ef7e927', url: 'https://github.com/KavyaSwSolutions-Ecommerce-project/Wallmart.git'
    }
    
    stage('Build'){
         sh "${mavenHome}/bin/mvn clean package" 
    }
    
    stage('Exceute SonarQube Report'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('UploadArtifact into Nexus'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    
    stage('Deploy app to Tomcat'){
        sshagent(['70436984-88b7-4a9b-af0b-863eca0dd6eb']){
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.215.159.88:/opt/apache-tomcat-9.0.118/webapps"
        }
    }
    
    stage('Email Notification'){
        emailext body: '''Buildd success
        Regards kavya''', subject: 'Build ovver of pipeline projects', to: 'kavyaraj313@gmail.com'
    }
    
    
}
