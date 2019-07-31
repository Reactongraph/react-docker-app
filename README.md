  Deploy React.js Application by Using Docker
  ===========================================


Steps of Docker set-up are as follow:-
---------------------------------------

1. sudo apt-get update
2. sudo apt-get remove docker docker-engine docker.io
3. sudo apt install docker.io
4. sudo systemctl start docker
5. sudo systemctl enable docker

Check docker is installed or not, run this command: <h5>sudo docker -v</h5>

Docker configure in your project(React.js) follow these steps:-
------------------------------------------------------

1. goto root directory of your project.
2. open terminal then type command: <h5>touch Dockerfile</h5>
3. Dockerfile file generated in your project directory, then paste these lines are as given below in the file, after paste these lines and save it.<br/>
#Stage 1<br/>
FROM node:8 as react-build<br/>
WORKDIR /app<br/>
COPY . ./<br/>
RUN yarn install --network-timeout 300000 --no-lockfile<br/>
RUN npm install --save rebuild-node-sass node-sass<br/>
RUN yarn run build --prod<br/><br/>
#Stage 2 - the production environment<br/>
FROM nginx:alpine<br/>
COPY --from=react-build /app/build /usr/share/nginx/html<br/>
EXPOSE 80<br/>
CMD ["nginx", "-g", "daemon off;"]<br/>


Build Docker Image by using this command:
-----------------------------------------
<h5>sudo docker build .(dot represent working directory) -t <name of project></h5>
&nbsp;&nbsp;&nbsp; Example:
<h5> sudo docker build . -t react-docker-app</h5>
&nbsp;&nbsp;&nbsp; or
<h5>sudo build -t react-docker-app . </h5> 

Then, run the docker images in your system by using this command:<br/>
<h5>sudo docker run -it -p 8000:80 react-docker-app</h5>
&nbsp;&nbsp;&nbsp; or
<h5>sudo docker run -it -p 8000:80 <Image ID></h5>

Open browser then type : localhost:8000, then application running of this port, If this is port occupied by other server, 
then you change port number at the time of docker image run. Example:
<h5>sudo docker run -it -p 9000:80 a9a4d1b08eed</h5>
&nbsp;&nbsp;:- a9a4d1b08eed this is docker image id
