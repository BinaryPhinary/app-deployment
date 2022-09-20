# mobile-eye-app-deployment

Pipeline files.

This is the final set of deployment files to put the mobile-eye app with the http service into kubernetes

The Jenkinsfile will perform the build - however it will only work with a Jenkins-slave - and only with the Jenkins kubernetes plugin.
At the top of the Jenkins file is the trigger for Jenkins to use the kubernetes plugin and try to spin up a jenkins-slave.


The mobile-eye app Dockerimage was previously created in the image creation pipeline.

The nodeport service is design to allow http traffic to hit the namespace.
