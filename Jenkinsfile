pipeline {
    agent any
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Выберите окружение')
    }
    stages {
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENV}"
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'localhost-ssh',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*',
                                    remoteDirectory: "deploy_${params.ENV}",
                                    execCommand: "echo 'Файлы успешно скопированы в /tmp/deploy_${params.ENV}'"
                                )
                            ]
                        )
                    ]
                )
            }
        }
        stage('Cleanup') {
            steps {
                echo "Очистка рабочей директории..."
                cleanWs()
            }
        }
    }
}