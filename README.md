<div align="center">
<img src="https://marketplace.deep-hybrid-datacloud.eu/images/logo-deep.png" alt="logo" width="300"/>
</div>

# DEEP-OC-ai4eosc_thunder_nowcast_ml
[![Build Status](https://jenkins.indigo-datacloud.eu/buildStatus/icon?job=Pipeline-as-code/DEEP-OC-org/DEEP-OC-ai4eosc_thunder_nowcast_ml/master)](https://jenkins.indigo-datacloud.eu/job/Pipeline-as-code/job/DEEP-OC-org/job/DEEP-OC-ai4eosc_thunder_nowcast_ml/job/master)

This is a container that will run [ai4eosc_thunder_nowcast_ml](https://github.com/MicroStep-MIS/ai4eosc_thunder_nowcast_ml) application leveraging the DEEP as a Service API component ([DEEPaaS API V2](https://github.com/indigo-dc/DEEPaaS)).

    
## Running the container

### Directly from Docker Hub
To run the Docker container directly from Docker Hub and start using the API
simply run the following command:

```bash
$ docker run -ti -p 5000:5000 -p 6006:6006 microstep/deep-oc-ai4eosc_thunder_nowcast_ml
```

This command will pull the Docker container from the Docker Hub [microstep](https://hub.docker.com/u/microstep/) repository and start the default command (deepaas-run --listen-ip=0.0.0.0).

**N.B.** For either CPU-based or GPU-based images you can also use [udocker](https://github.com/indigo-dc/udocker).


### Running via docker-compose
`docker-compose.yml` allows you to run the application with various configurations via docker-compose, for example:

```bash
$ docker-compose up ai4eosc_thunder_nowcast_ml
```

**N.B!** `docker-compose.yml` is of version '2.3', one needs docker 17.06.0+ and docker-compose ver.1.16.0+, see https://docs.docker.com/compose/install/

If you want to use Nvidia GPU, you need nvidia-docker and docker-compose ver1.19.0+ , see [nvidia/FAQ](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#do-you-support-docker-compose)


### Building the container
If you want to build the container directly in your machine (because you want to modify the `Dockerfile` for instance) follow the following instructions:
```bash
git clone https://github.com/MicroStep-MIS/DEEP-OC-ai4eosc_thunder_nowcast_ml
cd DEEP-OC-ai4eosc_thunder_nowcast_ml
docker build -t microstep/deep-oc-ai4eosc_thunder_nowcast_ml .
docker run -ti -p 5000:5000 -p 6006:6006 -p 8888:8888 microstep/deep-oc-ai4eosc_thunder_nowcast_ml
```

These three steps will download the repository from GitHub and will build the Docker container locally on your machine. You can inspect and modify the `Dockerfile` in order to check what is going on. For instance, you can pass the `--debug=True` flag to the `deepaas-run` command, in order to enable the debug mode.

## Connect to the API
Once the container is up and running, browse to `http://localhost:5000` to get
the [OpenAPI (Swagger)](https://www.openapis.org/) documentation page.


## Project structure
```
├─ Dockerfile             Describes main steps on integrationg DEEPaaS API and
│                         <your_project> application in one Docker image
│
├─ Jenkinsfile            Describes basic Jenkins CI/CD pipeline
│
├─ LICENSE                License file
│
├─ README.md              README for developers and users.
│
├─ docker-compose.yml     Allows running the application with various configurations via docker-compose
│
├─ metadata.json          Defines information propagated to the [DEEP Open Catalog](https://marketplace.deep-hybrid-datacloud.eu)
```

You can validate the `metadata.json` before making a git push using:
```shell
pip install git+https://github.com/deephdc/schema4apps
deep-app-schema-validator metadata.json
```
