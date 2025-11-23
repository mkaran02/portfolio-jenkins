pipeline {
    agent any
    
    environment {
        // Deployment directory on Windows IIS
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot\\portfolio'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                
                // Clone your GitHub repository
                git branch: 'main',
                    url: 'https://github.com/mkaran02/portfolio-jenkins'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Build Step: Checking project files'
                bat 'dir'      // Shows all files in Jenkins workspace
            }
        }
        
        stage('Deploy to IIS') {
            steps {
                echo 'Deploying files to IIS folder...'
                bat """
                    if not exist "${DEPLOY_DIR}" mkdir "${DEPLOY_DIR}"

                    echo Copying HTML files...
                    xcopy *.html "${DEPLOY_DIR}\\" /Y /E /I

                    echo Copying CSS files...
                    xcopy *.css "${DEPLOY_DIR}\\" /Y /E /I

                    echo Copying JS files (if exists)...
                    xcopy *.js "${DEPLOY_DIR}\\" /Y /E /I 2>nul

                    echo Deployment Completed Successfully.
                    
                    echo Final files in IIS folder:
                    dir "${DEPLOY_DIR}"
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully! Visit your website: http://localhost/index.html'
        }
        failure {
            echo 'Pipeline failed! Check build logs.'
        }
    }
}
