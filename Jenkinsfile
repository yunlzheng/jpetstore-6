node('swarm') {
    stage 'Checkout'
    git 'https://github.com/yunlzheng/jpetstore-6.git'

    stage 'Package'
    sh 'mvn clean package -DskipTests -DargLine="-Xmx1024m"'
    sh 'cp target/jpetstore.war docker/'
    dir('docker') {
      sh 'docker build -t jpetstore:$BUILD_NUMBER .'
    }

    stage 'Test'

    echo 'deploy app to TEST env'

    dir('docker') {
      sh '/usr/local/rancher-compose-v0.8.4/rancher-compose up -p PetStore-test --url http://192.168.50.102:8080 --access-key ACD7F882853FA5B96F03 --secret-key KHxC91gsw56mbbqBcit1jJasvTVCYU4DjL1ZD9Rs'
    }

    stage 'UAT'

    echo 'deploy app to UAT env'

    stage 'Prod'

    echo 'deploy app to Prod env'
}
