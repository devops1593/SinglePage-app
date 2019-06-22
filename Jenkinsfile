pipeline {
    
    agent 
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/devops1593/SinglePage-app.git'
            }
        }
        stage('Test') {
            steps {
                nvm(nvmInstallURL: 'https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh', 
             
                nvmIoJsOrgMirror: 'https://iojs.org/dist',
             
				nvmNodeJsOrgMirror: 'https://nodejs.org/dist', 
             
				version: '8.16.0')
				{
                   
					sh "npm install"
                    
					echo "Build main site distribution"
                    
					sh "npm run build"
             
				}
 
            }
        }
        stage('Deploy') {
            steps {
		sshPublisher(publishers: [sshPublisherDesc(configName: 'sonar', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'build', sourceFiles: 'build/**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])  
                
            }
        }
    }
}
