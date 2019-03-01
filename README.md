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

Or it will fail like this:
```
[INFO] --- docker-maven-plugin:0.27.2:start (psb-all) @ dmp-sample-helloworld ---
[INFO] DOCKER> [psb-all:latest] "psb-all": Start container bfdef268d7e9
[ERROR] DOCKER> [psb-all:latest] "psb-all": Container stopped with exit code 137 unexpectedly after 13191 ms while waiting on log out 'Hello World!'
[ERROR] DOCKER> Error occurred during container startup, shutting down...
[ERROR] DOCKER> Unable to remove container [bfdef268d7e9] : removal of container bfdef268d7e9 is already in progress (Conflict: 409) [removal of container bfdef268d7e9 is already in progress (Conflict: 409)]
```

with output from the other build like this:
```
[INFO] --- docker-maven-plugin:0.27.2:start (psb-all) @ dmp-sample-helloworld ---
[ERROR] DOCKER> Error occurred during container startup, shutting down...
[ERROR] DOCKER> I/O Error [Unable to create container for [psb-all] : Conflict. The container name "/build-2-psb-all-1" is already in use by container "e9fd98cd3a635b3f7a366b9d450ce126ea7ac7663f69fe3f9dac940906fdfd70". You have to remove (or rename) that container to be able to reuse that name. (Conflict: 409)]
```
