[![CircleCI](https://circleci.com/gh/rukykf/udacity-microservice-project.svg?style=svg)](https://circleci.com/gh/rukykf/udacity-microservice-project)

## Project Overview

The goal of this project was to put a machine learning microservice api (written in python) into a docker image, deploy that image to a kubernetes cluster and make requests to the api from outside the cluster.

The machine learning api is a pre-trained `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing).

## Setup the Environment

- Create a virtualenv and activate it
- Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone: `python app.py`
2. Run in Docker: `./run_docker.sh`
3. Run in Kubernetes: `./run_kubernetes.sh` (the image built for this project was pushed to a public repository so it will be available to Kubernetes)

### Kubernetes Steps

- Setup and Configure Docker locally
- Setup and Configure Kubernetes locally (for this project I used Minikube to setup a single node kubernetes cluster)
- Create Flask app in Container
- Run via kubectl

### Making Requests to the api

Make requests by running `./make_prediction.sh`
Note that requests are made to localhost on port 8000, so the local kubernetes cluster or docker container need to be publishing port 80 to 8000. The scripts provided for running the application in docker and kubernetes handle this port forwarding `./run_docker.sh` and `./run_kubernetes.sh`

### Files in the Repository

There are 3 main groups of files in this repository. The first group consists of the main application files `app.py` which contains the code for the api used to make predictions on housing prices and `requirements.txt` which contains a list of dependencies for pip to install.

The second group consists of utility scripts `./run_docker.sh` which copies and builds the application code into a docker image, `./update_docker.sh` which pushes the docker image to docker hub, `./run_kubernetes.sh` which deploys the docker image to the configured kubernetes cluster using kubectl and a `Makefile` which presents a clean list of make commands for activating the python environment and linting the code files in the repository.

The third maih group of files are in the `output_txt_files` directory and they are simply a record of log output from docker/kubernetes when the `./makde_prediction.sh` script is run
