node {

    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }

    stage('Clone repository') {
        checkout scm
    }

    stage('Twistlock Labs - CIS - Privileged pod created') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f priv-pod.yaml'
        }
    }

    stage('Twistlock Labs - CIS - Pod created in host process ID namespace') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f host-proc-id.yaml'
        }
    }

    stage('Twistlock Labs - CIS - Pod created on host IPC namespace') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f host-ipc.yaml'
        }
    }

    stage('Twistlock Labs - CIS - Pod created on host network') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f host-network.yaml'
        }
    }

    stage('Twistlock Labs - CIS - Privilege escalation pod created') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f escalation.yaml'
        }
    }

    stage('Twistlock Labs - Pod created with sensitive host file system mount') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl apply -f sensitive.yaml'
        }
    }

    stage("Wait 1 minute") {
            sh 'sleep 60'
    }

    stage('Cleanup Pods') {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'kubectl delete -f priv-pod.yaml'
            sh 'kubectl delete -f host-proc-id.yaml'
            sh 'kubectl delete -f host-ipc.yaml'
            sh 'kubectl delete -f host-network.yaml'
            sh 'kubectl delete -f escalation.yaml'
            sh 'kubectl delete -f sensitive.yaml'
        }
    }

    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }
}