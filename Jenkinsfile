pipeline {
    agent any {
        docker {
            image 'devopsjourney1/myjenkinsagents:python' 
        }
    }
    stages {
        stage('Preparação do Ambiente') {
            steps {
                echo 'ja instalado'
            }
        }

        stage('Execução do Teste Levenshtein') {
            steps {
                sh 'python3 levenshtein_teste.py'
            }
        }

        stage('Verificação do Arquivo de Perguntas') {
            steps {
                script {
                    if (fileExists('perguntas.txt')) {
                        echo 'Arquivo perguntas.txt encontrado!'
                    } else {
                        error('Arquivo perguntas.txt não encontrado. Interrompendo o pipeline.')
                    }
                }
            }
        }

        stage('Execução do Chatbot') {
            steps {
                sh 'python chat_bot.py'
            }
        }
    }
}
environment {
    PATH = "C:\\Windows\\System32;C:\\Usuários\\gabri\\AppData\\Local\\Programs\\Python\\Python312;C:\\Usuários\\gabri\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;${env.PATH}"
}