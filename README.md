The purpose of this article is to receive some testing feedback from engineers for a fix applied to the hooks script 03build.sh on the Single Docker container platform.

By default, Single Container Docker platform supports the exposure of only one port (if multiple ports are listed in the Dockerrun.aws.json file). Documentation quote: You can specify multiple container ports, but Elastic Beanstalk uses only the first one to connect your container to the host's reverse proxy and route requests from the public Internet


Please follow the steps listed below to test this workaround:

1) Create a Single Docker container environment using the Beanstalk Sample application

2) Using eb-cli or using the web console, upload the provided source bundle to the environment (Only use the  SingDockerPorts.zip source bundle, ignore the 03build3.sh as it is already present in S3 and available through the ebextensions in the source bundle)

  - Feel free to make changes to the Dockerrun.aws.json, add or subtract the ContainerPort objects

3) Once the deployment goes through, log in to the Beanstalk instances and run $ sudo docker ps; to confirm if all the container ports we exposed.

 - Based on the provided sample the result should be some thing like: 

5dc9961ce254        8de2280cdb7d        "nginx -g 'daemon of…"   25 seconds ago      Up 25 seconds       44/tcp, 80/tcp, 8080/tcp, 8084/tcp   flamboyant_heisenberg 


