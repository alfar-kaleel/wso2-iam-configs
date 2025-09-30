pipeline {
  agent any
  environment {
    SSH_CREDENTIALS_ID = 'wso2-ssh-key'                   
    IAM_HOME = '/Users/alfarkaleel/Wso2-Utils/Identity-servers/wso2is-5.11.0'
    DEPLOYMENT_FILE_PATH = '${IAM_HOME}/repository/conf/deployment.toml'

  }
  stages {

    stage('Checkout the branch') {
            steps {
                git branch: 'develop', url: 'https://github.com/alfar-kaleel/wso2-iam-configs.git'
            }
        }


    stage('Replace deployment.toml') {
            steps {
                echo "Going to copy deployment.toml"
                sh 'cp -f deployment.toml "$DEPLOYMENT_FILE_PATH"'
                echo "File copied"
            }
        }

  }
}