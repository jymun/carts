def label = "jenkins-docker-${UUID.randomUUID().toString()}" 
def registry = 'registry.dev-ops.kr/sockshop' 
 
podTemplate(label: label,   
    containers: [   
        containerTemplate(name: 'docker', image: 'docker', ttyEnabled: true, command: 'cat'), 
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.14.7', ttyEnabled: true, command: 'cat'), 
        containerTemplate(name: 'maven', image: 'maven', ttyEnabled: true, command: 'cat' ) 
    ],   
    volumes: [  
        hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
    ]  
)   
{  
    node (label) {   
 
        stage 'Checkout'  
            checkout scm  
         
        stage('compile') { 
                container('maven') { 
                   sh ("mvn -DskipTests package")   
                } 
            } 
             
     
        } 
    }   
}   
