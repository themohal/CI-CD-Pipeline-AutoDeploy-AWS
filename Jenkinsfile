node {
    def appDir = "/var/www/next-app"

    stage('Clean Workspace') {
        echo "Cleaning workspace"
        deleteDir()
    }

    stage('Clone Repository') {
        echo "Cloning repository"
        git branch: 'main',
            url: 'https://github.com/themohal/CI-CD-Pipeline-AutoDeploy-AWS.git'
    }

    stage('Deploy to EC2') {
        echo "Deploying application"

        sh """
        sudo mkdir -p ${appDir}
        sudo chown -R jenkins:jenkins ${appDir}

        rsync -av --delete 
        --exclude='.git' 
        --exclude='node_modules'
        ./ ${appDir}
        
        cd ${appDir}
        sudo npm install
        sudo npm run build
        sudo fuser -k 3000/tcp || true
        sudo npm start
        """
    }
}