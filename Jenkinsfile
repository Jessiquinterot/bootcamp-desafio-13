pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Construir la imagen Docker
                    bat 'docker build -t desafio13 "C:\\Users\\Usuario\\Desktop\\BOOTCAMP\\desafio 12"'
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    // Ejecutar el contenedor
                    bat 'docker run -d --name mi_contenedor desafio13'
                }
            }
        }
        stage('Testing') {
            steps {
                // Ejecutar las pruebas de la aplicación
               // bat 'pip install -r requirements.txt'  // Instalar dependencias de Python
                bat 'pytest'                           // Ejecutar pruebas con pytest
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    // Iniciar sesión en DockerHub
                    withCredentials([usernamePassword(credentialsId: 'Semeolvido-20', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'

                        // Etiquetar la imagen con tu nombre de usuario en DockerHub
                        bat 'docker tag desafio13 jessiquinterot/desafio13'

                        // Publicar la imagen en DockerHub
                        bat 'docker push jessiquinterot/desafio13'
                    }
                }
            }
        }
    }

    triggers {
        cron('H * * * *') // Esto ejecutará el pipeline cada hora
    }
}
