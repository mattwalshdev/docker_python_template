# Docker - Python Template
### Basic template for a single use python script based in Docker
This package lets the user build and run a Python script in Docker.  
Most examples I've found involve service runtimes eg. Flask or a database, but this package lets you build and run simple scripts with Docker and docker-compose.

It runs in a Python venv so if you want to work on the project, sans Docker it will run exactly the same.


## How to configure
1. rename docker_python_template folder to your app name
2. if you wish to rename the defaut run file from main.py do so now
3. Open Dockerfile and edit the below
   - `ARG VENV_PATH=/opt/.venv` (if you want to change venv folder)
   - `ARG APP_DIR=/usr/src/app/docker_python_template` (update app location)
   - `WORKDIR /usr/src/app` (if you changed the apps root folder structure above)
   - `#RUN apk add --no-cache gcc musl-dev linux-headers` (uncomment if Alpine Linux doesn't properly load certain pip libraries)
   - `CMD ["main.py"]` (if you changed the default python run file name)
4. If you want changes to reflect without rebuilding the container each time, then edit docker-compose.dev.yml, only if you changed the apps root folder strucutre


## How to run DEV
This will mount a volume on the container, so all changes are automatically available without a rebuild.

To run the default program  
`docker-compose -f docker-compose.dev.yml run --rm app-dev`  
To run any other file in the application  
`docker-compose -f docker-compose.dev.yml run --rm app-dev other.py`  


## How to run PROD
This will build without a volume mount and uses the default docker-compose.yml file.

To run the default program  
`docker-compose run --rm app`  
To run any other file in the application  
`docker-compose run --rm app other.py`  

If you want to update the contents of the PROD container  
`docker-compose build`
If you want to update the root contents of the DEV container (the app source folder is already mounted) 
`docker-compose -f docker-compose.dev.yml build`


## Running without Docker
cd to top level app dir  
`python3 -m venv .venv`  
`source .venv/bin/activate`  
`pip install --upgrade pip`  
`pip install --upgrade setuptools`
`pip install wheel`  
`pip uninstall -y pkg-resources` (Ubuntu only bug)  
For development and testing  
`pip install -r requirements.dev.txt`  
For production  
`pip install -r requirements.txt`  

:seedling: :seedling: :seedling: :seedling: :seedling: