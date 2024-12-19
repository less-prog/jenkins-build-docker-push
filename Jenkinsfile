node {
    def registryProjet = 'registry.gitlab.com/desiree.ziriga/formation-jedi-lesli'
    def IMAGE = "${registryProjet}:version-${env.BUILD_ID}"

    stage('Clone') {
        // Cloner le dépôt avec les identifiants appropriés
        git url: 'https://github.com/less-prog/jenkins-build-docker-push.git', credentialsId: 'reg'
    }

    def img
    stage('Build') {
        img = docker.build("$IMAGE", '.')
    }

    stage('Run') {
        img.withRun("--name run-${env.BUILD_ID} -p 80:80") { c ->
            sh 'curl localhost'
        }
    }

    stage('Push') {
        docker.withRegistry('https://registry.gitlab.com', 'reg1') {
            img.push('latest')
            img.push()
        }
    }
}
