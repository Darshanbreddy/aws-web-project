Tech Stack & Tools
AWS EC2 – Virtual server to host the app

AWS CodeArtifact – Maven repository for dependency management

AWS CodeBuild – For compiling and packaging the application

AWS CodeDeploy – For automated deployment to EC2

AWS CodePipeline – For complete CI/CD orchestration

AWS IAM – Role-based access control

AWS CloudFormation – Infrastructure as Code (IaC)

GitHub – Source code management

Apache Maven – Build automation

Shell Scripts – Deployment lifecycle management

Pipeline Workflow
The CI/CD pipeline begins by setting up AWS CodeArtifact as a secure Maven repository to manage and store application dependencies. An IAM policy was created with permissions to retrieve authorization tokens, read from the repository, and authenticate via AWS STS.

Using these credentials, the environment variable CODEARTIFACT_AUTH_TOKEN was exported to allow Maven to connect to CodeArtifact through a configured settings.xml file.

Once the build environment was ready, AWS CodeBuild was configured to clone the source code from GitHub and execute the buildspec.yml file, which compiles and packages the Java web application using Maven.

Following a successful build, AWS CodeDeploy was used to automate the deployment of the application onto an EC2 instance. This was managed through an appspec.yml file, which coordinated three shell scripts—install_dependencies.sh, start_server.sh, and stop_server.sh—to handle the lifecycle of the deployment process.

To streamline the entire process, AWS CodePipeline was set up to orchestrate all stages: pulling the latest source code from GitHub, triggering CodeBuild for compilation, and finally deploying the application through CodeDeploy. Rollback capabilities were also tested to ensure reliability.

To facilitate reusability and scalability, a CloudFormation template was created to define all necessary AWS resources, enabling quick setup of the environment in future iterations.

After testing the pipeline and ensuring successful deployments, all AWS resources were safely deleted to prevent incurring unnecessary charges.


