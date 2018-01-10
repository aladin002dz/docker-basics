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
> docker rmi image_code
```

### Remove Container
```
> docker rm container_code
```

### list runnning containers:
```
> docker ps
```

### stop a running docker container:
```
> docker stop image_code
```

### browse docker files:
```
> docker exec -it container_code bash
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
```
