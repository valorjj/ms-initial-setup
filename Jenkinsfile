node {
    stage('Github Checkout') {
        checkout([$class: "GitSCM",
            branches: [[name: "*/main"]],
            extensions: [],
            userRemoteConfigs: [[credentialsId: "git", 
            url: "https://github.com/valorjj/ms-initial-setup.git"]]
        ])
    }
    stage('Deploy to GKE') {
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: 'k8s/config-maps.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )

        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: 'k8s/mysql-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )

        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: 'k8s/redis-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )

        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: 'k8s/zipkin-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )
    }
}