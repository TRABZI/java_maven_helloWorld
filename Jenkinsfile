node {

    stage('Clone') {
        	git 'https://github.com/TRABZI/homeWork_TP_Jenkins_webhook_sonar.git'
    }


    stage('SonarQube analysis') {
        def scannerHome = tool 'sonar'
        withSonarQubeEnv('sonar'){
               sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=http://141.95.160.233:9000/ -Dsonar.projectName=project2 -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=jnknsSnrqb2  -Dsonar.sources=./ -Dsonar.language=java -Dsonar.java.binaries=."
        }
    }

    stage('Gate Quality'){
        def qualitygate = waitForQualityGate()
        if (qualitygate.status != "OK") {
                error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
        }
    }


    stage('Build') {
        	sh label: '', script: 'javac ./src/main/java/com/xavki/HelloWorld.java'
    }

    stage('Run') {
        	sh label: '', script: 'java ./src/main/java/com/xavki/HelloWorld'
    }

}
