# mobile-eye-app-deployment

Pipeline files.

This is the final set of deployment files to put the mobile-eye app with the http service into kubernetes

The Jenkinsfile will create the build.  The mobile-eye app image was previously created in the image creation pipeline.

The nodeport service is design to allow http traffic to hit the namespace.
