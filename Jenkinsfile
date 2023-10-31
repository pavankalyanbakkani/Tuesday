pipeline {
    agent {
        node {
            label 'built-in' // Use Jenkins' built-in node
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Hello, Worldddd! its a Tuesdayyyy'
            }
        }
    }
    
  stages {
        stage('Notify Sleuth') {
            steps {
                withCredentials([string(credentialsId: 'sleuth', variable: 'SLEUTH_API_KEY')]) {
                    script {
                        def response = httpRequest(
                            url: 'https://app.sleuth.io/api/1/deployments/testtoken/tuesday-3/register_deploy',
                            httpMode: 'POST',
                            contentType: 'APPLICATION_JSON',
                            authentication: 'SLEUTH_API_KEY',
                            validResponseCodes: '100:599' // this makes sure all responses are treated as valid
                        )
                        echo "Response from Sleuth: Status: ${response}"
                    }
                }
            }
        }
    }
}

