# DevOps with Docker 2019
## 1.1
![1.1 solution](/images/1_1_solution.png)

## 1.2
I have some images I will still use, so I won't remove all images, but I hope that removing the nginx image I won't be using will be enough and prove that I know how to remove images.
![1.2 solution](/images/1_2_solution.png)

## 1.3
The password is `basics` and the secret message is `This is the secret message`.
```
docker run -it devopsdockeruh/pull_exercise
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## 1.4
The secret message is "Docker is easy"
Commands given where
```
docker run -d devopsdockeruh/exec_bash_exercise
553c2d3ce22b091dacb866706794a351452493307cad9c2e350f2c47138aa54f
docker exec -it 55 bash
tail -f ./logs.txt
Sat, 11 Jan 2020 21:53:51 GMT
Sat, 11 Jan 2020 21:53:54 GMT
Sat, 11 Jan 2020 21:53:57 GMT
Sat, 11 Jan 2020 21:54:00 GMT
Secret message is:
"Docker is easy"
```

## 1.5
The command I used was:
```
docker run -i ubuntu sh -c 'apt-get update; apt-get install curl --assume-yes; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
```
So I added `-i` to wait for user input for the website and commands `apt-get update; apt-get install curl --assume-yes;` to the commands given in shell inside the container to install curl. Flag `--assume-yes` makes the installation not to wait for confirmation.

## 1.6
The Dockerfile can be found [here](1.6/Dockerfile). It's contents are:
```
FROM devopsdockeruh/overwrite_cmd_exercise

CMD ["--clock"]
```
The command used to build the image with the desired tag was `docker build -t docker-clock .`
The container can now be run with command `docker run docker-clock`.

## 1.7
The Dockerfile can be found [here](1.7/Dockerfile) and the script file [here](1.7/script.sh)
The contents of the Dockerfile are:
```
FROM ubuntu

RUN apt-get update && apt-get install -y curl
COPY script.sh .
RUN chmod a+x script.sh
CMD ./script.sh
```
and the contents of script.sh are:
```
echo "Input website:";
read website;
echo "Searching..";
sleep 1;
curl http://$website;
```
The image is built with command `docker build -t curler .` and the containter is run with command `docker run -it curler`.

## 1.8
The command I used in this exercise was
```
docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise
```

## 1.9
The command I used in this exercise was
```
docker run -p 80:80 devopsdockeruh/ports_exercise
```

## 1.10
The Dockerfile can be found [here](1.10/Dockerfile) and its contents are:
```
FROM ubuntu

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install git -y
RUN git clone https://github.com/docker-hy/frontend-example-docker.git
WORKDIR /frontend-example-docker
RUN npm install
EXPOSE 5000
CMD npm start
```
The container can then be run with command `docker run -p 5000:5000 [container name/id]`.

## 1.11
The Dockerfile can be found [here](1.11/Dockerfile) and its contents are:
```
FROM ubuntu

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install git -y
RUN git clone https://github.com/docker-hy/backend-example-docker
WORKDIR /backend-example-docker
RUN npm install
EXPOSE 8000
CMD npm start
```
And the correct command to start the container is: `backend-example-docker perttu$ docker run -p 8000:8000 -v $(pwd)/logs.txt://backend-example-docker/logs.txt [container id/name]`.

## 1.12
The altered Dockerfile for backend can be found [here](1.12/backend/Dockerfile) and for frontend [here](1.12/frontend/Dockerfile).

The content for the backend Dockerfile is:
```
FROM ubuntu

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install git -y
RUN git clone https://github.com/docker-hy/backend-example-docker
ENV FRONT_URL=http://localhost:5000
WORKDIR /backend-example-docker
RUN npm install
EXPOSE 8000
CMD npm start
```
and for the frontend Dockerfile:
```
FROM ubuntu

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install git -y
RUN git clone https://github.com/docker-hy/frontend-example-docker.git
ENV API_URL=http://localhost:8000
WORKDIR /frontend-example-docker
RUN npm install
EXPOSE 5000
CMD npm start
```
The commands to start the containers are the same as in previous exercises.