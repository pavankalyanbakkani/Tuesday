pipeline {
    agent {
        node {
            label 'built-in' // Use Jenkins' built-in node
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Hello, World! its a Tuesday'
            }
        }
    }
    
   post {
    success {
        script {
            def commitSHA = 'YOUR_SHA'  // Fetch this dynamically
            def authToken = 'Bearer YOUR_ACTUAL_ORG_REGISTER_DEPLOY_ACCESS_TOKEN' // Adjust the prefix (Bearer/Token) as required

            // Using curl as an alternative to httpRequest
            def response = sh(script: """
                curl -s -o /dev/null -w "%{http_code}" \\
                -X POST \\
                -H "Content-Type: application/json" \\
                -H "Authorization: ${authToken}" \\
                -d '{"environment": "production", "sha": "${commitSHA}"}' \\
                https://app.sleuth.io/api/1/deployments/testtoken/tuesday-2/register_deploy
            """, returnStdout: true).trim()

            echo "Response code from Sleuth: ${response}"

            if (response != '200') {
                error("Failed to register deployment with Sleuth!")
            }
        }
    }
}
