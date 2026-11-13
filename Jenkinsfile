pipeline {
    agent any

    environment {
        // Yeh wahi credential ID hai jo aapne Jenkins mein banaya hai
        VERCEL_TOKEN = credentials('vercel-token-id')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // GitHub webhook se aane wale code ko checkout karega
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Windows environment ke liye 'bat' command
                bat 'npm install'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Vercel CLI ke zariye production par deploy karega
                bat 'npx vercel --token %VERCEL_TOKEN% --prod --yes'
            }
        }
    }

    post {
        success {
            echo '✅ Vercel deployment kamyabi ke sath mukammal ho gayi hai!'
        }
        failure {
            echo '❌ Vercel deployment fail ho gayi hai. Upar logs check karein.'
        }
    }
}