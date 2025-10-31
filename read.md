step 1 : build the image using docker build command
docker build -t hello-devops .
# . will represent it will use the dockerfile for building the image
step 2 : 
once its ready then run as docker container
# docker run -d -p 5001:5001 hello-devops
step 3 :
check in localhost:5001 
