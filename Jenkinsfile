pipeline {
    agent none
    environment {
        DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
    }
    stages {
        stage('C# code') {
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk:5.0'}
            }
            steps {
                echo 'Build C# code'
                sh "dotnet build"
                echo 'Run C# Tests'
                dir("./DotnetTemplate.Web") { 
                    sh "dotnet test"
                }
            }
        }
        stage('TypeScript code') {
            agent {
                docker {image 'node:17-bullseye'}
            }
            steps {
                dir("./DotnetTemplate.Web") { 
                    echo 'Build TypeScript code'
                    sh "npm ci"
                    sh "npm run build"
                    echo 'Linting on TypeScript code'
                    sh "npm run lint"
                    echo 'Run TypeScript tests'
                    sh "npm t"
                }
            }
        }
    }
}

