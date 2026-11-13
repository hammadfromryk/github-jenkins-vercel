pipeline {
    agent any

    environment {
        // Jenkins Credentials mein sirf Vercel Token ki ID deni hai
        VERCEL_TOKEN = credentials('vercel-token-id')
    }

    triggers {
        // Jaise hi GitHub par code push hoga, ye pipeline auto-trigger ho jayegi
        githubPush()
    }

    stages {
        stage('Checkout Code') {
            steps {
                // GitHub repo se code fetch karega
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Project dependencies install karega
                sh 'npm install'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Vercel token ka use karke production par deploy karega 
                // (Ye project ki .vercel folder se automatically project aur org ID utha lega)
                sh '''
                    npx vercel --token $VERCEL_TOKEN --prod --yes
                '''
            }
        }
    }

    post {
        success {
            echo '🎉 Code successfully Vercel par deploy ho gaya hai!'
        }
        failure {
            echo '❌ Vercel deployment fail ho gayi hai. Logs check karein.'
        }
    }
}