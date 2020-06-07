node {

    withMaven(maven:'maven') {

        stage('Checkout') {
            git url: 'https://github.com/cweijiaweil-github/emartback.git', credentialsId: 'github-piomin', branch: 'master'
        }

        stage('Build') {
            sh 'mvn clean install'

            def pom = readMavenPom file:'pom.xml'
            print pom.version
            env.version = pom.version
        }

        stage('Image') {
            sh "docker build -t eureka:v1 ."
        }

        stage ('Run') {
            sh "docker run -p 9001:9001 eureka"
        }
     

    }

}