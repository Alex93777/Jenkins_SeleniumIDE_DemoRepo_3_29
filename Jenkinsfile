pipeline {
    agent any

    stages{
        stage("Checkout code"){
            //checkout the repository
            steps{
                git branch: 'main', url: 'https://github.com/Alex93777/Jenkins_SeleniumIDE_DemoRepo_3_29'
            }
        }
        stage("Set up .Net Core"){
            //install dot net
        }
        stage("Restore dependencies"){
            //install dependencies
        }
        stage("Build"){
            //build
        }
        stage("Run Tests"){
            //run tests
        }
    }
}