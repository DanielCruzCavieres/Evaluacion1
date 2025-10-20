// Inicia la definición del pipeline
pipeline {
    // 1. Agente: Indica a Jenkins dónde ejecutar el pipeline.
    // 'any' significa que lo ejecutará en cualquier agente disponible (en tu caso, el nodo principal).
    agent any

    // 2. Herramientas: Define las herramientas que se necesitan.
    tools {
        // Le pide a Jenkins que use la configuración de Maven que llamaste 'Maven-Default'.
        // ¡IMPORTANTE!: En Jenkins, ve a "Manage Jenkins" > "Global Tool Configuration"
        // > "Maven" > "Add Maven" y asegúrate de que el 'Name' sea exactamente 'Maven-Default'.
        maven 'Maven-Default'
        jdk 'JDK-21' 
    }

    // 3. Etapas: Define los pasos "en cascada" que te pide la evaluación.
    stages {

        // --- Etapa 1: Obtener código fuente de git ---
        stage('1. Checkout from Git') {
            steps {
                echo 'Obteniendo código desde GitHub...'
                // Clona tu repositorio desde la rama 'main'.
                git branch: 'main', url: 'https://github.com/DanielCruzCavieres/Evaluacion1.git'
            }
        }

        // --- Etapa 2: Realizar análisis del código ---
        stage('2. Analyze & Build') {
            steps {
                echo 'Ejecutando análisis, compilación y pruebas...'
                // 'bat' es el comando para ejecutar scripts de Windows (Batch).
                // 'mvn clean package' limpia, compila tu código, ejecuta las pruebas (análisis)
                // y empaqueta el resultado en un archivo .jar.
                bat 'mvn clean package'
            }
        }

        // --- Etapa 3: Realizar deployment ---
        stage('3. "Deployment" (Simulado)') {
            steps {
                echo 'Simulando el deployment...'
                // Para esta evaluación, "desplegar" será guardar el archivo .jar
                // que se generó en la etapa anterior.
                // Esto demuestra que el build fue exitoso.
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }

    // 4. Post-Acciones: Pasos que se ejecutan al final del pipeline.
    post {
        // 'always' se ejecuta siempre, ya sea que el pipeline falle o sea exitoso.
        always {
            echo 'Pipeline finalizado.'
        }
    }
}