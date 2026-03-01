node{
    def appDir = "/var/www/next-app/"
    stage('Cleanworkspace') {
        echo "Cleaning workspace"
        deleteDir()
    }
    stage('Clone repository') {
        echo "Cloning repository"
        git(
            branch: 'main',
            url: 'https://github.com/themohal/CI-CD-Pipeline-AutoDeploy-AWS.git'
            )
    stage('Deploy EC2') {
        echo "Deploying the application"
        sh """
        mkdir -p ${appDir}
        sudo chown -R 
        jenkins:jenkins ${appDir}
        rsync -av --delete --exclude='.git' 
        --exclude='node_modules' 
        ./ 
        ${appDir}
        cd ${appDir}
        sudo npm install
        sudo npm run build
        sudo fuser -k 3000/tcp
        sudo npm start &

        """
    }
        
}