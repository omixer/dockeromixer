### A development Angular image  

#### A typical development workflow 

```bash
VERSION=17.1.0
# chose a project name 
PROJECT_NAME=angular_project
CONTAINER_NAME=container_name

# create a new angular project
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app omixer/angular:${VERSION} new $PROJECT_NAME --routing=true --style=scss --commit=false --skip-git --strict --package-manager=yarn

# remove node module
cd $PROJECT_NAME
rm -rf node_modules package-lock.json

# replace by YARN
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app -p 4201:4200 --name ${CONTAINER_NAME} omixer/angular:${VERSION} config -g cli.packageManager yarn

# install dependencies 
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app --entrypoint yarn omixer/angular:${VERSION}

# start the container
docker run -it --rm -u $(id -u ${USER}):$(id -g ${USER}) -v ${PWD}:/app -p 4201:4200 --name ${CONTAINER_NAME} omixer/angular:${VERSION} serve --host 0.0.0.0
```