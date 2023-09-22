# Use the miniconda parent image
FROM continuumio/miniconda3:22.11.1

# Copy the environment.yml file to the container
COPY environment.yml .
RUN conda env create -f environment.yml

# Activate the Conda environment
RUN echo "source activate a2-env" >> ~/.bashrc
ENV PATH /opt/conda/envs/a2-env/bin:$PATH

#Create a non-root user and use that user
RUN useradd -m assignment
USER assignment

# Set the working directory
WORKDIR /home/assignment

# Expose the JupyterLab port
EXPOSE 8888

# Launch JupyterLab when the container starts
CMD ["jupyter", "lab", "--ip=0.0.0.0"]


#docker run -it -p 8888:8888 -v /Users/macbookpro/geog313-assignments/assignment-2:/home/assignment assign2_image
