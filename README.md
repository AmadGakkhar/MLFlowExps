# MLFlowExps



# Using DagsHub

MLFLOW_TRACKING_URI=https://dagshub.com/AmadGakkhar/MLFlowExps.mlflow \
MLFLOW_TRACKING_USERNAME=AmadGakkhar \
MLFLOW_TRACKING_PASSWORD=c895d600eeedba2cc913cd87e089f87f7ac1f68e \
python script.py


''' bash

export MLFLOW_TRACKING_URI=https://dagshub.com/AmadGakkhar/MLFlowExps.mlflow
export MLFLOW_TRACKING_USERNAME=AmadGakkhar
export MLFLOW_TRACKING_PASSWORD=c895d600eeedba2cc913cd87e089f87f7ac1f68e

'''

# MLFlow on AWS Setup

1. Login to console.
2. Create IAM User with Administrator access.
3. Export credentials in your AWS CLI by running **aws configure.**
4. Create s3 bucket.
5. Create EC2 Machine (Ubuntu) and add security groups (5000 port).
    Select instance -> Goto security -> Select security group -> Edit inbound rules -> Add rules -> Add port number 5000 and select 0.0.0.0/0 -> Save rules

Run the following commands on EC2 Machine

''' bash
sudo apt update
sudo apt install python3-pip
sudo pip3 install pipenv
sudo pip3 install virtualenv
mkdir mlflow
cd mlflow
pipenv install mlflow
pipenv install awscli
pipenv install boto3
pipenv shell
aws configure

mlflow server -h 0.0.0.0 --default-artifact-root s3://mlflow-bucket-2623

Open public IPv4 DNS to port 5000

Set uri in local terminal and in your code

export ML_FLOW_TRACKING_URI=http://ec2-3-142-248-17.us-east-2.compute.amazonaws.com:5000

update remote_server_uri in your code as well to see the tracking on aws server.