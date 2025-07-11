pipeline{
    agent any

    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                    dockerImage = docker.build("thisisfeeder/netflix", "--build-arg TMDB_V3_API_KEY=012d807f181b715c75ca72d866b0fd38 .")
                    sh 'docker login -u thisisfeeder -p dckr_pat_ohVtE7M7iIdALy2dY0GyXqNAZPo'
                    sh 'docker push thisisfeeder/netflix'

                }
            }
        }
        stage('Deploy to docker swarm'){
            steps{
                script{
                    sh 'docker stack deploy -c docker-compose.yml netflix'
                }
            }
        }
    }
}
