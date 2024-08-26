# update to the latest version of all packages
FROM ubuntu:latest

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install python3 -y
RUN apt-get install python3-pip -y
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED
RUN pip3 install flask

WORKDIR /app
# Copy the api.py file to /app directory inside the Docker image
COPY ./api.py /app/api.py

# Exposer le port 5252
EXPOSE 5252

CMD ["python3", "api.py"]
