# Jenkins-Test
Jenkins-test is my first project intended to learn about some DevOps tools such as Jenkins, Sonarqube and Docker.

## Composition
* **Docker** - Folder where configuration and necessary files to run the system are stored. Note that you have to use your own jenkins key to connect to the slave as it is password protected.
* **PythonHelloWorld** - Folder with a basic Python Flask API solution and its unit tests.
* ***ROOT***
  * **Jenkins files** - Files with Jenkins pipelines, separating branches from master branch.
  * **README.md** - This file!
  * **sonar-project.properties** - File with configuration to execute Sonarqube analysis during master build.


## Usage
### Docker containers
To run the containers with Jenkins, its Slave and Sonarqube, you just need to execute:
```bash
docker-compose up --build -d
```

When you want to stop the system, just execute:
```bash
docker-compose down
```
And all the containers will be stopped and destroyed. Don't worry about the data because it is persistent in the created volumes.

Note that you would have to configure each tool separately, I mean, set Jenkins up, add the slave node to it, install plugins, connect it with Sonarqube, etc.

### Python solution
As said, it is only a basic Python app which runs a listener in the port 9999. Using curl, any browser or a rest client, you can get the result.
Being Python 3 previously installed, just execute:
```bash
python hello_world.py
```
And to query the API:
```bash
curl http://127.0.0.1:9999/helloworld
```

## Deployment
The master Jenkinsfile has been updated with a new step to deploy the solution in a Docker container.

I created the file 'Dockerfile_Deployment' to build the image. Basically it copies the Python app and install the required libraries.

When a branch is merged to master, Jenkins builds the image and pushes it onto my own [registry](https://cloud.docker.com/u/davidleonm/repository/docker/davidleonm/pythonhelloworld).

The version is located in the 'VERSION' file. It must be modified manually, I thought about auto-tagging with Jenkins but I think that Jenkins should be readonly. Furthermore, all the Github repositories are configured to allow only signed commits, if Jenkins is able to commit and push, it would imply a secuity breach.

## Changelog
* **1.0.0** - Updated the pipelines to deploy the solution after merging to master.
* **First release** - First release with a working suite of DevOps tools and a basic Python solution.


## License
Use this code as you wish! Totally free to be copied/pasted.