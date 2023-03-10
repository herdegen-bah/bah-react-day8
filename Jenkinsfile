node {
    
    stage ("Checkout React Client"){
        git branch: 'main', url: 'https://github.com/herdegen-bah/bah-react-day8.git'
    }
    
    stage ("Install dependencies - react client") {
        sh 'npm install'
    }
	stage("Delete previous env - react client"){
		sh 'kubectl delete deployment react-day7 || true'
		sh 'kubectl delete service react-day7 || true'
	}
    
    stage('User Acceptance Test - react client') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {
	    stage('Deploy to Kubernetes cluster - react client') {
	      sh "kubectl create deployment react-day7 --image=settlagekl/react-day7:v1.0"
	      sh "kubectl expose deployment react-day7 --type=LoadBalancer --port=80"
	    }
	  }
    }

    stage("Production Deployment View"){
        sh "kubectl get deployments"
        sh "kubectl get pods"
        sh "kubectl get services"
    }
}
