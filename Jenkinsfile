node{

  //Define all variables
  def project = 'wordpress_app'
  def imageVersion = 'v2.0'
  def namespace = "${namespace_gui}"
  def imageTag = "wordpress:v11.1"

  //Checkout Code from Git
  checkout scm

  //Stage 1 : Build the docker image.
        stage('Build image') {
            sh("docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD")
            sh("docker build -t nagaraj1171/${imageTag} . --no-cache")
        }
    //Stage 2 : Testing the code.
        stage('Testing the code') {
            sh("echo Testing......")
            sh("echo Testing Done")
        }

    //Stage 3 : Push the image to docker registry
        stage('Push image to registry') {
            sh("docker push nagaraj1171/${imageTag}")
        }
    //Stage 3 : Cleaning
            stage('Cleaning Old docker and k8 images') {
                //sh("kubectl delete -f .")
                //sh("chmod +x run_destroy.sh")
                //sh("./run_destroy.sh")
                //sh('''docker rmi $(docker images -f 'dangling=true' -q) || true
                    //docker rmi $(docker images | sed 1,2d | awk '{print "\$3"}') || true''')
            }

    //Stage 4 : Deploy Application

              stage('Deploy Application To K8 Cluster') {
                   sh("echo $namespace")
                   switch (namespace) {
                          //Roll out to Dev Environment
                          case "development":
                          //sh ("kubectl apply -f wordpress-volumeclaim.yaml")

                          // Create Contentful Service
                          sh("ls")
                                sh("kubectl apply -k .")
                                //sh("kubectl create -f wordpress.yaml")
                                //sh ("kubectl get pod -l app=wordpress")
                                //sh("kubectl create -f wordpress-service.yaml")
                                //sh ("kubectl get svc -l app=wordpress")
                                //sh ("if [ `kubectl get pods -o=wide|grep Running | awk '{print \$3}'` = "Running" ]; then `kubectl get pod -l app=wordpress`; sleep 5; else echo "Not Running"; fi"
                                //sh('''while [ ''kubectl get pods -o=wide|grep Running | awk '{print "\$3"}''' != 'Running' ]; do kubectl get pod -l app=wordpress; sleep 5; done''')

                          // Check for Service
                                sh("minikube service wordpress --url")
                                sh("kubectl get pods -o=wide")
                                sh("NAME=`minikube service list|grep wordpress |awk '{print ''\$''6}'`")
                                sh("hostname")
                            }
      }
  }
