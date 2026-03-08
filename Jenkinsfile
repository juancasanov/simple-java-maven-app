pipeline {
    agent { label 'agent1' }
    parameters {
        choice(name: 'RAMA_A_COMPILAR', 
               choices: ['master', 'declarative', 'testng'], 
               description: 'Selecciona la rama del repositorio de GitHub')
    }
    stages {
        stage('Limpieza y Verificación') {
            steps {
                script {
                    def folderName = 'simple-java-maven-app'
                    if (fileExists(folderName)) {
                        echo "SALIDA CONSOLA: La carpeta ${folderName} YA existe. Eliminando..."
                        sh "rm -rf ${folderName}"
                    }
                }
            }
        }
        stage('Descarga') {
            steps {
                sh "git clone -b ${params.RAMA_A_COMPILAR} https://github.com/jenkins-docs/simple-java-maven-app.git"
            }
        }
        stage('Compilación') {
            steps {
                dir('simple-java-maven-app') {
                    sh 'mvn clean install'
                }
            }
        }
    }
}
