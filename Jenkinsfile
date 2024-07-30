pipeline {
    agent any

    stages {
        stage("Checkout Code"){
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/DimoLitov/JenkinsSeleniumWebDriver_30.07'
            }
        }
   
        stage("SetUp Dotnet core"){
            //checkout the repository
            steps {
                bat '''
                echo Downloading .Net 6 sdk
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/0c82e7e6-fdde-49f2-a69f-bd986aeafe1b/9ea7411a22e661fff0e61e56a466e484/dotnet-sdk-6.0.132-win-x64.exe
                echo installing dotnet-sdk-6.0.132-win-x64.exe
                dotnet-sdk-6.0.132-win-x64.exe /quiet /norestart
                '''
            }
        }

        stage("Restoring nuget packages"){
            //checkout the repository
            steps {
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }

        stage("Build"){
            //checkout the repository
            steps {
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }

        stage("Run Tests TestProject1"){
            //checkout the repository
            steps {
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

        stage("Run Tests TestProject2"){
            //checkout the repository
            steps {
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

        stage("Run Tests TestProject3"){
            //checkout the repository
            steps {
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
        
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}