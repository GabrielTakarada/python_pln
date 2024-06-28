pipeline {
    agent any

    environment {
        PATH = "C:\\Windows\\System32;C:\\Users\\gabri\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\gabri\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;${env.PATH}"
        TEMP_FILE = "chatbot_output.txt"
    }

    parameters {
        string(name: 'PERGUNTA', defaultValue: '', description: 'Digite a pergunta para o chatbot')
    }

    stages {
        stage('Preparação do Ambiente') {
            steps {
                echo 'ja instalado'
            }
        }

        stage('Execução do Teste Levenshtein') {
            steps {
                bat 'python levenshtein_teste.py'
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
                bat "python chat_bot.py \"${params.PERGUNTA}\" > ${env.TEMP_FILE}"
            }
        }
    }

    post {
        always {
            script {
                def resposta = readFile("${env.TEMP_FILE}").trim()
                emailext (
                    subject: "Resposta do Chatbot",
                    body: "A resposta para a pergunta '${params.PERGUNTA}' é:\n${resposta}",
                    to: "gabrieltakarada@gmail.com",
                    attachLog: true
                )
            }
        }
    }
}
