node {
    stage('Github Checkout') {
        checkout([$class: "GitSCM",
            branches: [[name: "*/main"]],
            extensions: [],
            userRemoteConfigs: [[credentialsId: "git", 
            url: "https://github.com/valorjj/ms-initial-setup.git"]]
        ])
    }

    stage('Deploy') {
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: 'k8s/',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true])
    }
}