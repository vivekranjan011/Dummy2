node {
    def gitRepo = 'https://github.com/vivekranjan011/Dummy2.git'
    def branch = 'main'
    def mavenHome = tool name: 'MAVEN3', type: 'maven'
        stage('Checkout') {
            echo 'Checking out code from Git repository...'
            git branch: branch, url: gitRepo
        }

        stage('Build') {
            echo 'Running build...'
            bat 'call App.bat'
        }

        stage('Test') {
            echo 'Running tests...'
            bat 'call Test.bat'
        }

        stage('Deploy') {
            echo 'Sending notification...'
            bat 'mvn -version'
    
        }
}
