node {
    stage('Github Checkout') {
        checkout([$class: "GitSCM",
            branches: [[name: "*/main"]],
            extensions: [],
            userRemoteConfigs: [[credentialsId: "git", 
            url: "https://github.com/valorjj/ms-initial-setup.git"]]
        ])
    }

    stage('Deploy to GKE: config-maps') {
        // config-maps
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: './k8s/config-maps.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )
    }

    stage('Deploy to GKE: mysql') {
        // mysql
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: './k8s/mysql-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )
    }

    stage('Deploy to GKE: zipkin') {
        // zipkin
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: './k8s/zipkin-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )
    }

    // ERROR: jenkins not reading this value
    // redis-deployment.yml -> causing error
    // 
    stage('Deploy to GKE: redis') {
        // redis
        step([$class: 'KubernetesEngineBuilder',
            projectId: env.PROJECT_ID,
            clusterName: env.CLUSTER,
            location: env.ZONE,
            manifestPattern: './k8s/redis-deployment.yml',
            credentialsId: env.GOOGLE_SERVICE_ACCOUNT_CREDENTIAL,
            verifyDeployments: true]
        )
    }

}