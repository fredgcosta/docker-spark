# Running a Spark cluster locally using docker 
This demo were presented in PAPIs Connect São Paulo 2017 (http://www.papis.io/connect-sao-paulo-2017/). It runs a Spark standalone cluster locally by means of docker containers. It also starts a MongoDB container (visible within the Spark cluster)

# $docker build spark --tag spark:2.1.0
First step: build Spark image

# $docker-compose up -d
Start containers (in detached mode, running containers in the background) for running MongoDB and a Spark Cluster (based on the image built previously). The Spark cluster simulates a master machine and a slave machine. 

# $docker-compose scale spark-scala=K
More slave machines may be started. “K” is the number of machines(i.e: containers) to start.

# $docker-compose logs <container-id>
It may be useful for analyzing the log of a specific container.

# $docker-compose exec spark-master spark-submit --class <main-class> spark://spark-master:6066 --deploy-mode cluster <application-jar>
Example of running a Java application within Spark.

# $docker exec -it <container-id of the master machine> /bin/bash
You can access the container and submit the same jar there.

# $spark-submit --class <main-class> spark://spark-master:6066 --deploy-mode cluster <application-jar>
Alternatively, you can run the same application directly inside the container.

# $docker-compose down
In order to shut down all containers.

# Check your Spark jobs
http://localhost:8080
