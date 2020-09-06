podTemplate(
  serviceAccount: 'jenkins',
  containers: [
    containerTemplate(
      name: 'maven',
      image: 'maven:3-jdk-8',
      resourceLimitMemory: '300Mi',
      ttyEnabled: true,
      command: 'cat'
    )
  ],
  volumes: [
    hostPathVolume(mountPath: '/root/.m2', hostPath: '/tmp/.m2')
  ]
)

{
    node(POD_LABEL) {
        stage('git scm update'){
                git 'https://github.com/gnu-gnu/simple-java-app-jib-2.git'
        }
        stage('packaing'){
            container('maven'){
                sh 'export MAVEN_OPTS=-Xmx300m; mvn clean jib:build -Dimage.tag=$BUILD_NUMBER'
            }
        }
    }
}
