FROM python:3

MAINTAINER Thiago Salvatore <thiago.salvatore@gmail.com>

RUN apt-get update && apt-get upgrade -y -q

RUN apt-get install -y locales

RUN locale-gen pt_BR.UTF-8  
ENV LANG pt_BR.UTF-8  
ENV LANGUAGE pt_BR.UTF-8
ENV LC_ALL pt_BR.UTF-8

# Set an environment variable to store where the app is installed to inside
# of the Docker image. The name matches the project name out of convention only.
ENV INSTALL_PATH /flask

RUN mkdir -p $INSTALL_PATH

# This sets the context of where commands will be ran in and is documented
# on Docker's website extensively.
WORKDIR $INSTALL_PATH


# Ensure packages are cached and only get updated when they change. This will
# drastically decrease build times when your packages do not change.
COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

# Copy in the application code from your work station at the current directory
# over to the working directory.
COPY . .

CMD uwsgi --ini uwsgi.ini

