pipeline {
    agent any
    
    stages {
        stage('Check Branch') {
            steps {
                script {
                    if (env.BRANCH_NAME != 'feature-ci-pipeline') {
                        currentBuild.result = 'ABORTED'
                        error("Pipeline only runs on feature-ci-pipeline branch. Current branch: ${env.BRANCH_NAME}")
                    }
                    echo "Running on correct branch: ${env.BRANCH_NAME}"
                }
            }
        }
        
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Restore dependencies') {
            steps {
                bat 'dotnet restore Homies.sln'
            }
        }
        
        stage('Build solution') {
            steps {
                bat 'dotnet build Homies.sln --no-restore'
            }
        }
        
        stage('Run Unit Tests') {
            steps {
                bat 'dotnet test **/*UnitTests.csproj --no-build --verbosity normal'
            }
        }
        
        stage('Run Integration Tests') {
            steps {
                bat 'dotnet test **/*IntegrationTests.csproj --no-build --verbosity normal'
            }
        }
    }
}
