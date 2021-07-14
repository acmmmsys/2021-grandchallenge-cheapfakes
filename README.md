# MMSys'21 Grand Challenge on Cheapfakes

Challenge homepage: https://2021.acmmmsys.org/cheapfake_challenge.php  
Overview paper: https://arxiv.org/abs/2107.05297


## Retrieving the public dataset 

Please request access to the public dataset by filling out the form [here](https://forms.gle/kTY4cZPfFKCG35YLA). 

Note that by agreeing to the terms of use, you also agree to **follow the guidelines provided in the challenge description and not to use any dataset or material other than those explicitly provided for the challenge, in building your detector**.


## Original paper and source code

We refer readers to this [paper](https://arxiv.org/abs/2101.06278) and [GitHub repository](https://github.com/shivangi-aneja/COSMOS) for background information on the COSMOS study. Please note that these are for information purposes only: you can participate in the challenge without relying on the training strategy proposed in or any artifacts from the original study.


## Submitting your Docker image

To submit your Docker image, you need to do the following:
1. Install Docker
2. Create a Dockerfile
3. Build a Docker image from your Dockerfile
4. Test your Docker image
5. Upload your Docker image


### 1. Installing Docker

Go to https://docs.docker.com/get-docker/ and install the Docker application corresponding to your platform.


### 2. Creating your Dockerfile

- **Decide on the base image.** For instance, you can consider using an existing [nvidia/cuda image](https://hub.docker.com/r/nvidia/cuda/tags): 

```
FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04
```

- **Install additional dependencies.** Examples:

```
RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y <some package>
RUN apt-get install <some package>
RUN apt-get -y install <some package>
```

- **Copy necessary files.** Copy necessary files from local path to container path. For instance, for `/mmsys21cheapfakes` as the target directory in the container:

```
COPY <local files> /mmsys21cheapfakes
```

Further commands for installing dependencies, which refer to the container path, can be added after this operation:

```
RUN pip3 install -r /mmsys21cheapfakes/requirements.txt
```

- **Designate the code entrypoint.** For instance, if the file called `awesome-model.py` should be run using `python3`:  

```
CMD [ "python3", "awesome-model.py" ]
```

You can visit https://docs.docker.com/develop/develop-images/dockerfile_best-practices/ for more comprehensive documentation on creating a Dockerfile.


### 3. Building your Docker image

- Go to the folder where your Dockerfile resides.

- To build an image named `<container name>`, run the following command: 

```
docker build -t <container name> .
```

- To build an image named `<container name>` and tagged `<container tag>`, run the following command: 

```
docker build -t <container name>:<container tag> .
```

You can visit https://docs.docker.com/engine/reference/commandline/build/ for more comprehensive documentation on building a Docker image.


### 4. Testing your Docker image

Assuming that the relevant test split file `test.json` resides in the local folder `<submission folder>`, you can run the following command to test your Docker image:

```
docker run -v <submission folder>:/mmsys21cheapfakes [OPTIONS1] <container name> [OPTIONS2]
```

(See below for the exact command that will be run by the organization committee during evaluation.)


### 5. Uploading your Docker image

Please upload your Docker image to [DockerHub](https://hub.docker.com/) with the container name `mmsys21cheapfakes`. Use the tag `submission` for the version you would like to be evaluated. Example for a Dockerhub user called `<username>`:

```
SOURCE=<container name>
TARGET='<username>/mmsys21cheapfakes'
TAG='submission'
docker login
docker tag ${SOURCE} ${TARGET}:${TAG} && docker push ${TARGET}:${TAG}
```

You can omit the tag for intermediate versions before the submission:

```
SOURCE=<container name>
TARGET='<username>/mmsys21cheapfakes'
docker login
docker tag ${SOURCE} ${TARGET} && docker push ${TARGET}
```


## Evaluation

Participant models will be run using the following command: 

```
docker pull <username>/mmsys21cheapfakes:submission
docker run -v <path to folder containing the hidden test split file test.json>:/mmsys21cheapfakes --gpus all mmsys21cheapfakes:submission > <output file>
```
