# Devops_Proj_5_Counter_App
This is a demo Devops project demonstrating a CI/CD Pipeline

There are two Jenkin files, one to perform CI and one to perform CD

Continuous Intgeration:

In the CI Jenkins file, a pipeline script was written using Maven to perform unit tests, perform integration
tests and to build the project

The resulting build was then sent to SonarQube for static code analysis, where it was also analyzed by a quality gate

After passing the tests of SonarQube and quality gate, the project was uploaded to Nexus, with one that is the project and one as a snapshot

Finally, the project was created into an image using a Dockerfile and pushed to DockerHub

Continuous Deployment:

In the CD Jenkins file, parameters were first written to paramatize the inputs to connect to AWS EKS

After connecting to AWS EKS, the project was deployed using Kubernetes.

In the CD pipeline, there is an option to either create or destroy the deployment. The user selects 
the option on Jenkins to determine what to do with the deployment