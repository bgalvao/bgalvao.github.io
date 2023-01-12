---
title: "Get the right container log from a Docker Swarm service"
date: 2022-01-12
draft: false
tags: ["misc", "devops", "docker", "docker swarm"]
---

In Docker Swarm, a history of containers is kept throughout the lifecycle of the Docker Stack.
Sometimes, you need to look into a service to know if it's behaving as it should.
However, if the service has been restarted 3 times, or if it is replicated, if you run a
`docker service logs prefect_agent`, you will get a mumbo-jumbo of logs of all containers,
regardless whether they're running or not.

Thus, in the first place you should first:

```shell
docker service ps prefect_agent
# alternatively
docker service ps prefect_agent --format "table {{ .ID }}\t{{ .Name }}\t{{ .Status }}"
```

and you will get a nicely formatted list of all containers running under that service name.
They are characterized by the host where they are running, and whether they are running or dead.

So, pick the one that you're interested in, and take its ID or name, and you will get
a log from a single container with

```shell
docker logs <ID or container name>
```

Cheers.

