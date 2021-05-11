pipeline {

  agent any
  
  environment {
    //adding a comment for the commit test
    ANYPOINT_CREDS = credentials('ANYPOINT_CREDENTIALS')
   
  }
  
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('Deployment') {
     
     environment {
        CLIENT_ID = credentials('DEV_CLIENT_ID')
        CLIENT_SECRET = credentials('DEV_CLIENT_SECRET')
   
      }
      
      steps {
            bat 'mvn -U -V -e -B -DskipTests -Pdev deploy  -DmuleDeploy -Dusername="%ANYPOINT_CREDS_USR%" -Dpassword="%ANYPOINT_CREDS_PSW%" -Dclient_id="%CLIENT_ID%" -Dclient_secret="%CLIENT_SECRET%"'
      }
    }
    
  }

  
}