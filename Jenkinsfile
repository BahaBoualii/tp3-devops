pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    echo '📥 Checking out code from GitHub...'
                    // Le checkout est automatique avec "Pipeline script from SCM"
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    echo '☸️ Deploying to Kubernetes...'
                    
                    // Vérifier la connexion
                    sh 'kubectl cluster-info'
                    sh 'kubectl get nodes'
                    
                    // Déployer les manifests
                    sh 'kubectl apply -f k8s/deployment.yaml'
                    sh 'kubectl apply -f k8s/service.yaml'
                    
                    // Redémarrer pour forcer le pull de la dernière image
                    sh 'kubectl rollout restart deployment/my-app-deployment'
                    
                    // Attendre que le rollout soit terminé
                    sh 'kubectl rollout status deployment/my-app-deployment --timeout=3m'
                    
                    echo '✅ Deployment completed!'
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    echo '🔍 Verifying deployment...'
                    sh 'kubectl get pods -l app=my-app'
                    sh 'kubectl get svc my-app-service'
                    
                    echo '🌐 Application accessible via http://localhost:8080'
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline executed successfully!'
            sh 'kubectl get all -l app=my-app'
        }
        failure {
            echo '❌ Pipeline failed!'
            sh 'kubectl describe pods -l app=my-app || true'
            sh 'kubectl logs -l app=my-app --tail=50 || true'
        }
    }
}