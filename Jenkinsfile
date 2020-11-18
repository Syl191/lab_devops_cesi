pipeline {
  agent any
  stages {
    stage('Create Dockerfile') {
      steps {
        sh '''# Creation du Dockerfile
touch Dockerfile

# Renseignement du Dockerfile
echo "FROM nginx:alpine
COPY index.html /usr/share/nginx/html
" >> Dockerfile

echo "Check dockerfile"
cat Dockerfile

echo ""
echo "Check index.html"
cat index.html'''
      }
    }

    stage('Docker image') {
      steps {
        sh '''# Build Docker Image 
docker build -t registerme:latest .
'''
        sh '''# Upload to the local registry
docker tag registerme:latest registry.me:5000/registerme:latest 
docker push registry.me:5000/registerme:latest '''
      }
    }

    stage('Launch Web Site') {
      steps {
        sh '''# Run docker website
docker run --name registerme -d -p 80:80 registry.me:5000/registerme:latest'''
      }
    }

  }
}