pipeline {
    agent any

    tools {
        nodejs 'Node_js'
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {

        stage('Hello App') {
            steps {
                echo 'Apple Product Showcase CI/CD pipeline started'
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shohail-DeV/Apple-Product-Showcase.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Test') {
    steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
            bat 'npm test'
        }
    }
}


        stage('Build Application') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }

        // stage('Deploy to Vercel (Production)') {
        //     environment {
        //         VERCEL_TOKEN = credentials('VERCEL_TOKEN')
        //     }
        //     steps {
        //         echo 'Deploying Vite app to Vercel Production'

        //         bat '''
        //         npm install -g vercel
        //         vercel pull --yes --environment=production --token=%VERCEL_TOKEN%
        //         vercel build --prod --token=%VERCEL_TOKEN%
        //         vercel deploy --prebuilt --prod --token=%VERCEL_TOKEN%
        //         '''
        //     }
        // }
    }

    post {
        success {
            echo 'Production deployment successful'
        }
        failure {
            echo 'Pipeline failed — investigate immediately'
        }
    }
}
