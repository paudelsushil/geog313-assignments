<h1>Running the Jupyter lab using the docker file </h1>

## Install Docker:
​
 **Install Docker on the computer. Docker's official website can be found [here](https://docs.docker.com/desktop/install/mac-install/)**

 ## Creating the environment.yml file
 We can create this using any text editor.
​
## Creating Dockerfile
Create the directory name **assignment-2** and inside the directory create **Dockerfile** in which we have to write following python codes.

```python linenos
# use miniconda parent image
<FROM continuumio/miniconda3:22.11.1 #<continuumio.miniconda is name of parent image:<this is the version>>
​
# Copy the environment.yml file into the container
COPY environment.yml .  #should not missed this last dot with space.
RUN conda env create -f environment.yml #This code will run the create the conda environment having the name specified in yml file.
​
# Activate the Conda environment
RUN echo "conda activate a2-env" >> ~/.bashrc #<a2-env is the name of the conda environment that we have created using environmnet.yml file>
ENV PATH="$PATH:/opt/conda/envs/a2-env/bin" #This is the path of conda environment.
​
# Create a non-root user and switch to that user
RUN useradd -m assignment #<sushil is the name for non-root user>
USER assignment
​
# Set the working directory to /home/jupyteruser
WORKDIR /home/assignment #this is the directory inside the docker container which always initialized with /home/<user> "which can be non-root or root user"
​
# Expose the JupyterLab port
EXPOSE 8888
​
# Start JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0"]>
```

## Building Image using Dockerfile
- We will need to open a terminal to navigate to our Dockerfile directory; in my case i.e. assignment2. A Docker image can be built with the following command.

```python linenos
docker build -t assign2_image .
```
## Running the Docker container
​
- By running the following command after building the image, we can create and run a container:

```python linenos
docker run -it -p 8888:8888 -v /Users//geog313-assignments/assignment-2:/home/assignment assign2_image
```
​
*docker run* : We use this to run a Docker container using the image that is specified at the end of the code.
​
*-p 8888:8888*: is mapped from the container to the host machine via port 8888. 
​
*-v /Users/macbookpro/geog313-assignments/assignment-2:/home/assignment*: Mounting is created by this flag. My host machine's directory (/Users/macbookpro/geog313-assignments/assignment-2) is bound to a container's directory (/home/assignment). 

In this case, our host and container can share files or data using this technique.
​
**assign2_image* : Docker image name
​
​
## Running the Jupyter Lab ### 
​
- We will receive a [Link](http://127.0.0.1:8888/lab?token=b00ad6a7401545d8c06857462bd17358ff45cf0c190372da) 
 If we open this link using browser we will be able to access jupyter lab and container.