def label = "jenkins-docker-${UUID.randomUUID().toString()}" 
def imageurl = 'registry.dev-ops.kr/sockshop:latest' 
 
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
             
      stage ('docker build') {
	      		container('docker') { 
            sh ("docker build -t registry.dev-ops.kr/sockshop:latest .")
            writeFile file: 'anchore_images', text: imageurl
            anchore name: 'anchore_images'
	 	       	
		     	}
	   	}
        
    }   
}   
