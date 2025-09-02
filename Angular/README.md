### A development Angular image  

#### A typical development workflow 

```bash
VERSION=17.1.0
# chose a project name 
PROJECT_NAME=angular_project
CONTAINER_NAME=container_name

# create a new angular project
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app omixer/angular:${VERSION} new $PROJECT_NAME --routing  --ssr --zoneless --style=scss --commit=false --skip-git --strict --package-manager=yarn

# start the container
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app -p 4201:4200 --name ${CONTAINER_NAME} omixer/angular:${VERSION} serve --host 0.0.0.0
```