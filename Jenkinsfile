pipeline{
	
	agent any
	
	environment {
	  DEPLOY_CREDS = credentials('deploy-anypoint-user')
	  MULE_VERSION = '4.2.2'
	  BG = "MST Solutions"
	  WORKER = "Micro"
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
		stage('Deploy Development') {
			environment {
				ENVIRONMENT = 'Dev'
				APP_NAME = 'mule4-batch-demo'
			}
			steps {
				bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy
				-Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%"
				-Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%"
				-Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%"
				-Dcloudhub.worker="%WORKER%"'
			}
		}
		stage('Deploy Production') {
			environment {
				ENVIRONMENT = 'Production'
				APP_NAME = 'mule4-batch-demo'
			}
			steps {
				bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy
				-Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%"
				-Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%"
				-Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%"
				-Dcloudhub.worker="%WORKER%"'
			}
		}
    }
	
	tools {
		maven 'M3'
	}
}
  