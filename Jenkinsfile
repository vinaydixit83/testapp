pipeline {
    agent any

    environment {
        DOTNET_HOME = "C:\\Program Files\\dotnet" // Adjust the path for .NET SDK on your local Jenkins server
        PATH = "C:\\Users\\vinay\\source\\repos\\sampleapi\\Publish"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/vinaydixit83/testapp.git'
            }
        }

stage('Restore packages') {
  steps {
      echo 'Restore packages...'
    bat "dotnet restore C:\\Users\\vinay\\source\\repos\\sampleapi\\sampleapi.sln"
  }
}


         stage('Build') {
            steps {
                echo 'Building the application...'
                bat 'C:\\Program Files\\dotnet\\dotnet.exe" build --configuration Release'
            }
        }

         stage('publish') {
            steps {
                script {
                    bat '"%DOTNET_HOME%\\dotnet.exe" publish --configuration Release --output C:\\Users\\vinay\\source\\repos\\sampleapi\\Publish'
                }
                //echo 'Building the application...'
            }
        }

        //stage('Run Tests') {
           // steps {
             //   echo 'Running unit tests...'
             //  sh 'dotnet test'
            //}
       // }

         stage('Deploy') {
            steps {
                echo 'Publishing the application...'
                bat 'dotnet publish -c Release -o publish'

                echo 'Starting the application on localhost...'
                bat 'start cmd /c dotnet publish\\sampleapi.dll'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
