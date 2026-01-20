Branch indexing
11:00:01 Connecting to https://api.github.com using noababliki71-ux/****** (GitHub access for Jenkins)
Obtained Jenkinsfile from e5b0f89f64e5a5888ef7109040bf17ec2e9488d2
[Pipeline] Start of Pipeline
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Init variables)
[Pipeline] node
Running on Jenkins in /var/jenkins_home/workspace/calculator-app-multibranch_main
[Pipeline] {
[Pipeline] checkout
The recommended git tool is: NONE
using credential github-creds
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/calculator-app-multibranch_main/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/noababliki71-ux/calculator-app-noa.git # timeout=10
Fetching without tags
Fetching upstream changes from https://github.com/noababliki71-ux/calculator-app-noa.git
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
using GIT_ASKPASS to set credentials GitHub access for Jenkins
 > git fetch --no-tags --force --progress -- https://github.com/noababliki71-ux/calculator-app-noa.git +refs/heads/main:refs/remotes/origin/main # timeout=10
Checking out Revision e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 (main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 # timeout=10
Commit message: "Part D - Fix ECR push (aws-cli image)"
 > git rev-list --no-walk ddb6bd644d1fccb8f46b925e66989e57a2035cd8 # timeout=10

Could not update commit status. Message: {"message":"Resource not accessible by personal access token","documentation_url":"https://docs.github.com/rest/commits/statuses#create-a-commit-status","status":"403"}

[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] echo
IMAGE_TAG resolved to: main-5
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build Docker Image)
[Pipeline] node
Running on Jenkins in /var/jenkins_home/workspace/calculator-app-multibranch_main
[Pipeline] {
[Pipeline] checkout
The recommended git tool is: NONE
using credential github-creds
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/calculator-app-multibranch_main/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/noababliki71-ux/calculator-app-noa.git # timeout=10
Fetching without tags
Fetching upstream changes from https://github.com/noababliki71-ux/calculator-app-noa.git
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
using GIT_ASKPASS to set credentials GitHub access for Jenkins
 > git fetch --no-tags --force --progress -- https://github.com/noababliki71-ux/calculator-app-noa.git +refs/heads/main:refs/remotes/origin/main # timeout=10
Checking out Revision e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 (main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 # timeout=10
Commit message: "Part D - Fix ECR push (aws-cli image)"

Could not update commit status. Message: {"message":"Resource not accessible by personal access token","documentation_url":"https://docs.github.com/rest/commits/statuses#create-a-commit-status","status":"403"}

[Pipeline] withEnv
[Pipeline] {
[Pipeline] isUnix
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ docker inspect -f . docker:27-cli
.
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] withDockerContainer
Jenkins seems to be running inside container 82a1b3ac80bfdce810d738e5e1953be83d0d31ad1c03edaf316a5f243cc1b436
$ docker run -t -d -u 0:0 -v /var/run/docker.sock:/var/run/docker.sock -w /var/jenkins_home/workspace/calculator-app-multibranch_main --volumes-from 82a1b3ac80bfdce810d738e5e1953be83d0d31ad1c03edaf316a5f243cc1b436 -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** docker:27-cli cat
$ docker top c17ac5680637b32e5698e527ba536ff4dbe03fb0e58ebc598bf1702dce8eafd1 -eo pid,comm
[Pipeline] {
[Pipeline] sh
+ docker build -t 992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app:main-5 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 187B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/python:3.11-slim
#2 DONE 0.6s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [1/5] FROM docker.io/library/python:3.11-slim@sha256:5be45dbade29bebd6886af6b438fd7e0b4eb7b611f39ba62b430263f82de36d2
#4 resolve docker.io/library/python:3.11-slim@sha256:5be45dbade29bebd6886af6b438fd7e0b4eb7b611f39ba62b430263f82de36d2 0.0s done
#4 DONE 0.0s

#5 [internal] load build context
#5 transferring context: 73.22kB 0.0s done
#5 DONE 0.1s

#6 [2/5] WORKDIR /app
#6 CACHED

#7 [3/5] COPY requirements.txt .
#7 CACHED

#8 [4/5] RUN pip install --no-cache-dir -r requirements.txt
#8 CACHED

#9 [5/5] COPY . .
#9 DONE 0.1s

#10 exporting to image
#10 exporting layers 0.1s done
#10 exporting manifest sha256:2c93be89a5b4871de512a1a10d67829336b1eb904844f88d71d1b111a2230746
#10 exporting manifest sha256:2c93be89a5b4871de512a1a10d67829336b1eb904844f88d71d1b111a2230746 0.0s done
#10 exporting config sha256:69b69db848ad9e3ca26c403252505b9d358db6da51da7d79aebb7565ed71f94a 0.0s done
#10 exporting attestation manifest sha256:3a80ae0a19928ee32086964c379872b08a91310f6848d6e5eb4b4302c4f7adf0 0.0s done
#10 exporting manifest list sha256:1dc8e109a16dec1de0e141da9fc18c6cc9f89ad1be83d8f299cf288e90142ff3 0.0s done
#10 naming to 992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app:main-5
#10 naming to 992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app:main-5 done
#10 unpacking to 992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app:main-5 0.0s done
#10 DONE 0.3s
+ docker images
+ grep calculator-app
992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app   main-5    1dc8e109a16d   1 second ago     211MB
992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app   main-4    1421f3ec901b   6 minutes ago    211MB
992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app   pr-2-3    9ac9ea430e9f   14 minutes ago   211MB
calculator-app                                                pr-2-2    fe09a6b468f6   2 hours ago      211MB
[Pipeline] }
$ docker stop --time=1 c17ac5680637b32e5698e527ba536ff4dbe03fb0e58ebc598bf1702dce8eafd1
$ docker rm -f --volumes c17ac5680637b32e5698e527ba536ff4dbe03fb0e58ebc598bf1702dce8eafd1
[Pipeline] // withDockerContainer
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push Image to ECR (main only))
[Pipeline] node
Running on Jenkins in /var/jenkins_home/workspace/calculator-app-multibranch_main
[Pipeline] {
[Pipeline] checkout
The recommended git tool is: NONE
using credential github-creds
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/calculator-app-multibranch_main/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/noababliki71-ux/calculator-app-noa.git # timeout=10
Fetching without tags
Fetching upstream changes from https://github.com/noababliki71-ux/calculator-app-noa.git
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
using GIT_ASKPASS to set credentials GitHub access for Jenkins
 > git fetch --no-tags --force --progress -- https://github.com/noababliki71-ux/calculator-app-noa.git +refs/heads/main:refs/remotes/origin/main # timeout=10
Checking out Revision e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 (main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f e5b0f89f64e5a5888ef7109040bf17ec2e9488d2 # timeout=10
Commit message: "Part D - Fix ECR push (aws-cli image)"

Could not update commit status. Message: {"message":"Resource not accessible by personal access token","documentation_url":"https://docs.github.com/rest/commits/statuses#create-a-commit-status","status":"403"}

[Pipeline] withEnv
[Pipeline] {
[Pipeline] isUnix
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ docker inspect -f . amazon/aws-cli:2.15.57

Error: No such object: amazon/aws-cli:2.15.57
[Pipeline] isUnix
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ docker pull amazon/aws-cli:2.15.57
2.15.57: Pulling from amazon/aws-cli
d83d4388ed12: Pulling fs layer
4280ad3170dc: Pulling fs layer
5e290d3fa940: Pulling fs layer
c9438aea349a: Pulling fs layer
bcf8bdfdd2dc: Pulling fs layer
d83d4388ed12: Download complete
c9438aea349a: Download complete
4280ad3170dc: Download complete
5e290d3fa940: Download complete
bcf8bdfdd2dc: Download complete
bcf8bdfdd2dc: Pull complete
4280ad3170dc: Pull complete
c9438aea349a: Pull complete
5e290d3fa940: Pull complete
d83d4388ed12: Pull complete
Digest: sha256:44d35524921b60e99ed7d6b7adc6135cc28ab16797739ead6ea62cee7b56a1b6
Status: Downloaded newer image for amazon/aws-cli:2.15.57
docker.io/amazon/aws-cli:2.15.57
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] withDockerContainer
Jenkins seems to be running inside container 82a1b3ac80bfdce810d738e5e1953be83d0d31ad1c03edaf316a5f243cc1b436
$ docker run -t -d -u 0:0 -v /var/run/docker.sock:/var/run/docker.sock -w /var/jenkins_home/workspace/calculator-app-multibranch_main --volumes-from 82a1b3ac80bfdce810d738e5e1953be83d0d31ad1c03edaf316a5f243cc1b436 -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** amazon/aws-cli:2.15.57 cat
$ docker top 3dab9e6cd94e0665f01d8abb66a03602e78bb27cac666a18b07e97a2cd8c1d00 -eo pid,comm
ERROR: The container started but didn't run the expected command. Please double check your ENTRYPOINT does execute the command passed as docker run argument, as required by official docker images (see https://github.com/docker-library/official-images#consistency for entrypoint consistency requirements).
Alternatively you can force image entrypoint to be disabled by adding option `--entrypoint=''`.
[Pipeline] {
[Pipeline] sh
+ aws ecr get-login-password --region us-east-1
+ docker login --username AWS --password-stdin 992382545251.dkr.ecr.us-east-1.amazonaws.com
/var/jenkins_home/workspace/calculator-app-multibranch_main@tmp/durable-7cb8f9ff/script.sh.copy: line 2: docker: command not found
