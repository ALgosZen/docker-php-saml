# docker-php-saml
# Title: ## Run Php inside docker and integrate simple saml 

### step 1 : clone repo or create dir structure with docker 

![Directory Structure](/images/dir.png?raw=true "Directory Structure")

### > docker compose has two services precisely app and nginx . both points to host volume for the php dir.
### > php:8.0.2-fpm docker image is used 
### > nginx.conf configures php root and various other settings for the webserver
### > to start - run from root: docker compose up
### > to stop - docker compose down
### > modify your preferred localhost port , ive set to 8008
### > verify app running going to http://localhost:8008
