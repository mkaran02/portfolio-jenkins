pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mkaran02/portfolio-jenkins'
            }
        }

        stage('Build') {
            steps {
                echo 'No build required for HTML/CSS'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website...'
                powershell """
                Remove-Item -Recurse -Force C:\\portfolio-deploy\\* 2>$null
                Copy-Item -Path * -Destination C:\\portfolio-deploy -Recurse -Force
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
    }
}
