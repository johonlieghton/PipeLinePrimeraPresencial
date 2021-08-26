pipeline {
  agent any
  stages {
    stage('Paso 1 Constructor App') {
      steps {
        echo 'Iniciamos la construccion de nuestra app'
        timestamps() {
          echo 'Marca de tiempo inicial'
        }

        sh 'sh ejecutar_constructor_script.sh'
        mail(subject: 'Estamos aqui', body: 'arranco el jenkins')
      }
    }

    stage('Prueba en Linux') {
      steps {
        echo 'Iniciando la prueba de Linux'
        sh 'sh ejecutar_test_para_linux.sh'
        sleep 5
        timestamps() {
          echo 'Finalizo la ejecucion de la prueba Linux'
        }

      }
    }

    stage('Confirmacion Manual de la Prueba Linux') {
      steps {
        echo 'Aguardando la confirmacion Manual'
        input 'La prueba de Linux resulto Ok?'
        timestamps() {
          echo 'Se recibio la confirmacion manual'
        }

      }
    }

    stage('Despliegue en Produccion') {
      steps {
        echo 'Desplegando en Produccion'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'gp1304@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}