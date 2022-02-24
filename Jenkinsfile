pipeline
{
agent any 
tools
{
// insatall the maven version configured as "m3" and add it to the path.
jdk 'Java 8'
maven "Maven 3.3.9"
}

stages 
{
stage('checkout')
{
steps
{
// get some code from a github repository
git url: 'https://github.com/kosurumuniraja/achu.git'
}
}
stage ('compile and Build') {

    steps {
        sh '''
        mvn clean install -U -Dmaven.test.skip=true
        '''
        
    }
}
stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('SonarQube') {
           sh '''
           mvn clean package org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=false
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" -Dsonar.sourceEncoding=UTF-8
           '''
           }
         }
      }    
}

}


