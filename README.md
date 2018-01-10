# Docker basics:
## Terms:
**Image:** ordered collection of root filesystem changes and the corresponding execution parameters
 for use within a container runtime. Images are read-only:  
	- https://docs.docker.com/glossary/?term=image
	
**Container:** active (or inactive if exited) stateful instantiation of an image:  
	- https://docs.docker.com/glossary/?term=container


## Docker usual commands
### Remove Image
```
> docker rmi image_id
```

### Remove Container
```
> docker rm container_id
```

### list runnning containers:
```
> docker ps
```

### stop a running docker container:
```
> docker stop container_id
```

### browse running container files:  
```
> docker exec -it container_id bash	
```

### check if docker is running:   
```
> docker run hello-world
```

If you are getting error, first go and check the docker daemon is running or not,  
```
> service docker status
```

if not running start the docker by running,  
```
> service docker start
```

### troubleshooting exited container:  
```
docker logs container_id
```

### browse image files:  
```
docker run --rm -it --entrypoint=/bin/bash image_id
```

### stop and delete all containers:  
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

### upload images to docker hub:  
```
docker login
docker push user_id/image_id
```
### download images from docker hub: 
```
docker login
docker pull user_id/image_id
```

## Example Docker with ASP.NET Core:
### Make app using .net core:
```
> mkdir AspNetCoreHelloWorld
> cd AspNetCoreHelloWorld
> dotnet new mvc --name webapp-name
```
```
> dotnet restore
> dotnet run
```

### Dockerfile:
```
		FROM microsoft/dotnet:latest
		COPY . /app
		WORKDIR /app
		 
		RUN ["dotnet", "restore"]
		RUN ["dotnet", "build"]
		 
		EXPOSE 5000/tcp
		ENV ASPNETCORE_URLS http://*:5000
		 
		ENTRYPOINT ["dotnet", "run"]
```

### Build and run:
```
> docker build -t mydemos:aspnetcorehelloworld .
> docker run -d -p 8080:5000 -t mydemos:aspnetcorehelloworld
> curl localhost:8080
```
