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
               echo Downloading .Net 6 Sdk
               curl -l -o https://builds.dotnet.microsoft.com/dotnet/Sdk/6.0.136/dotnet-sdk-6.0.136-win-x64.exe
               echo installing dotnet-sdk-6.0.132-win-x86.exe
               dotnet-sdk-6.0.132-win-x86.exe /quiet /norestart
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