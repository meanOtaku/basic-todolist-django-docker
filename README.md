# basic-todolist-django-docker
django project in a docker container for easy deployment and replacement 

pip install django

django-admin startproject mysite


cd djangoapp
vi requirements.txt



#requirements.txt
Django==1.9
gunicorn==19.6.0

#in dockerfile

# set the base image 
FROM python:2.7
# File Author / Maintainer
MAINTAINER Esther
#add project files to the usr/src/app folder
ADD . /usr/src/app
#set directoty where CMD will execute 
WORKDIR /usr/src/app
COPY requirements.txt ./
# Get pip to download and install requirements:
RUN pip install --no-cache-dir -r requirements.txt
# Expose ports
EXPOSE 8000
# default command to execute    
CMD exec gunicorn djangoapp.wsgi:application --bind 0.0.0.0:8000 --workers 3


 
Open your prefered text editor and your scp explorer in mycase winscp.
Locate to the folder
mysite/mysite/settings.py
and change
 ALLOWED_HOSTS  = [‘0.0.0.0’] 
docker build -t django_application_image .

docker run -p 8000:8000 -i -t django_application_image

and the test container for the django project is ready

Create a file name template in the file mysite 
main/template/main
this file will hold the html file for your project
now for the database create a folder 
/register outside mysite preferably you could create a folder for holding both register and mysite together and change the location will not matter much.
