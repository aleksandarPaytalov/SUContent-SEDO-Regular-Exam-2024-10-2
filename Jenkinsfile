pipeline {
    agent any
    
    when {
        branch 'feature-ci-pipeline'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Debug folder structure') {
            steps {
                bat 'dir /s'
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
