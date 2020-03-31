pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
         }
      }
    stage('Application Build') {
         steps {
            git 'https://github.com/BharathLinganna/spring-jenkins-project.git'
            sh label: '', script: 'mvn clean package -DskipTests'
         }
      }
      stage('Application_Unit_Test'){
         steps {
            sh label: '', script: 'mvn -Dfilename=testng-unit.xml test'
         }
	  post {
  	    always {
		    step([$class: 'Publisher'])
  	        }
          }
       }
       stage('Application_Code_Analaysis'){
         steps {
            sh label: '', script: 'mvn sonar:sonar'
         }
	   }
	   stage('Application_Deployment') {
         steps {
            sh label: '', script: 'cp $(pwd)/target/spring-project.war ~/jenkins-training/tomcat/webapps/'
            }
	    }
	    stage('Application_Functional_Test') {
            steps {
	            sleep time: 30, unit: 'NANOSECONDS'
                sh label: '', script: 'mvn -Dfilename=testng-functional.xml test'
            }
            post {
  	            always {
		        step([$class: 'Publisher'])
  	            }
        }
	    }
     }
}
