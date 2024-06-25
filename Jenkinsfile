pipeline {
    agent none
    stages {
        stage('Preparação do Ambiente') {
            agent {
                docker {
                    image 'devopsjourney1/myjenkinsagents:python'
                    label 'docker-agent-python' 
                }
            }
            steps {
                echo 'ja instalado'
            }
        }

        stage('Execução do Teste Levenshtein') {
            agent {
                docker {
                    image 'devopsjourney1/myjenkinsagents:python'
                }
            }
            steps {
                sh 'python3 levenshtein_teste.py'
            }
        }

        stage('Verificação do Arquivo de Perguntas') {
            agent {
                docker {
                    image 'devopsjourney1/myjenkinsagents:python'
                }
            }
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
            agent {
                docker {
                    image 'devopsjourney1/myjenkinsagents:python'
                }
            }
            steps {
                sh 'python chat_bot.py'
            }
        }
    }
}
