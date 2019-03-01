# demp-concurrent-stop

Run two commands with a little bit of delay from one another.
```
mvn verify -Ddocker.containerNamePattern='build-1-%n-%i'
mvn verify -Ddocker.containerNamePattern='build-2-%n-%i'
```

The build will fail like this:
```
[INFO] --- docker-maven-plugin:0.27.2:start (psb-all) @ dmp-sample-helloworld ---
[INFO] DOCKER> [psb-all:latest] "psb-all": Start container f91eac86eedb
[ERROR] DOCKER> Error occurred during container startup, shutting down...
[ERROR] DOCKER> Unable to stop container id [f91eac86eedb] : No such container: f91eac86eedb (Not Found: 404) [No such container: f91eac86eedb (Not Found: 404)]
```

With output from other build like this:
```
[INFO] --- docker-maven-plugin:0.27.2:stop (stop) @ dmp-sample-helloworld ---
[INFO] DOCKER> [psb-all:latest]: Stop and removed container f91eac86eedb after 0 ms
```
