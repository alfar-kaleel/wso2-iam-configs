pipeline {
  agent any
  environment {
    SSH_CREDENTIALS_ID = 'wso2-ssh-key'                   
    IAM_HOME = '/Users/alfarkaleel/Wso2-Utils/Identity-servers/wso2is-5.11.0'
    DEPLOYMENT_FILE_PATH = '/Users/alfarkaleel/Wso2-Utils/Identity-servers/wso2is-5.11.0/repository/conf/deployment.toml'

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

    stage('Restart WSO2 IAM') {
      steps {
        sshagent (credentials: [env.SSH_CREDENTIALS_ID]) {
          sh """
            set -e
            cd ${IAM_HOME}/bin
            echo "Stopping WSO2 server..."
            sh wso2server.sh stop || true
            echo "Successfully stopped  WSO2 IAM server..."
            sleep 15
            echo "Going to start WSO2 IAM server..."
            JENKINS_NODE_COOKIE=dontKillMe nohup ./wso2server.sh start &
            echo "Successfully started  WSO2 IAM server..."
            """
           
        }
      }
    }   


  }
}