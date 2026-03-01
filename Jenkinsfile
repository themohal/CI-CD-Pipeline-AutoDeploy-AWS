node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/themohal/CI-CD-Pipeline-AutoDeploy-AWS'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            # Install app dependencies
            sudo npm install

            # Build the app
            sudo npm run build

            # Delete old pm2 process if exists
            pm2 delete next-app || true

            # Start the Next.js app using pm2
            pm2 start npm --name "next-app" -- start

            # Save pm2 process list (for auto-restart)
            pm2 save
        """
    }
}