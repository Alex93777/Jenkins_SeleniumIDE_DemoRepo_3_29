pipeline {
    agent any

    stages {
        stage("Checkout code") {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Alex93777/Jenkins_SeleniumIDE_DemoRepo_3_29'
            }
        }

        stage("Download .Net SDK") {
            //checkout the repository
            steps {
               bat '''
               echo Downloading .Net 8 Sdk
               curl -L -o dotnet-sdk-8.0.310-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/4fbba4d2-246b-4f69-bc1d-9003ca0c5a43/c05954d6dd791067764a9599d5fabe30/dotnet-sdk-8.0.310-win-x64.exe
               echo installing dotnet-sdk-8.0.310-win-x64.exe
               dotnet-sdk-8.0.310-win-x64.exe /quiet /norestart
               '''
            }
        }

        stage("Restore Dependencies") {
            //checkout the repository
            steps {
               bat 'dotnet restore SeleniumIde.sln'
            }
        }

        stage("Build") {
            //checkout the repository
            steps {
               bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }

        stage("Run Tests") {
            //checkout the repository
            steps {
               bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: "**/TestResults/*.trx", allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}