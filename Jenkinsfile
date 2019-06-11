node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello-kenzan"
    registryHost = "ksr1729/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName
   
    stage "Build"
        sh "mkdir /tmp/s2i"
        sh "wget -q -P /tmp/s2i https://github.com/openshift/source-to-image/releases/download/v1.1.14/source-to-image-v1.1.14-874754de-linux-amd64.tar.gz"
        sh "docker build -t ${imageName} -f applications/hello-kenzan/Dockerfile applications/hello-kenzan"
    
    stage "Push"
        sh "docker login -u ksr1729 -p pass123!"
        sh "docker push ${imageName}"
        
        
            
    stage "Deploy"

        //kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'

}
