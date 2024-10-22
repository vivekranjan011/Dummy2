node {
    // Define variables
    def gitRepo = 'https://github.com/vivekranjan011/Dummy2.git'
    def branch = 'main'
    def emailRecipient = 'youremail@example.com'

    try {
        // Stage: Checkout
        stage('Checkout') {
            echo 'Checking out code from Git repository...'
            checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]],
                      userRemoteConfigs: [[url: gitRepo]]])
        }

        // Stage: Build
        stage('Build') {
            echo 'Running build...'
            bat 'call Test.bat'
        }

        // Stage: Test
        stage('Test') {
            echo 'Running tests...'
            bat 'call run_tests.bat'
        }

        // Stage: Notify Success
        stage('Notify') {
            echo 'Sending notification...'
            mail to: emailRecipient,
                 subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful. Check it at: ${env.BUILD_URL}"
        }

    } catch (Exception e) {
        // Stage: Notify Failure
        stage('Notify Failure') {
            echo 'Sending failure notification...'
            mail to: emailRecipient,
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build has failed. Please check it at: ${env.BUILD_URL}\n\nError: ${e.message}"
        }
        // Rethrow the exception to mark the build as failed
        throw e
    }
}
