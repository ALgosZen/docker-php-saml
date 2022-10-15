# docker-php-saml
# Title: ## Run Php inside docker and integrate simple saml 

### step 1 : clone repo or create dir structure with docker 

![Directory Structure](/images/dir.png?raw=true "Directory Structure")

#### > docker compose has two services precisely app and nginx . both points to host volume for the php dir.
#### > php:8.0.2-fpm docker image is used 
#### > nginx.conf configures php root and various other settings for the webserver
#### > to start - run from root: docker compose up
#### > to stop - docker compose down
#### > modify your preferred localhost port , ive set to 8008
#### > verify app running going to http://localhost:8008
## Now ready to configure SimpleSAMLPhp plugin
https://www.lewisroberts.com/2015/09/05/single-sign-on-to-azure-ad-using-simplesamlphp/

step 1. setup SAML Azure AD SSO for your PHP web application using SimpleSAMLphp
In the app registrations in Azure AD, select your app and click on endpoints. Copy the Federation metadata document. The federation metadata should be imported to your application.

The Identifier, Reply URL and Sign on URL should be configured in the Azure AD.

Identifier (Entity ID) : Enter a URL that uses the following pattern: 'https://.yourdomain.com' You can find this value as the Issuer element in the AuthnRequest (SAML request) sent by the application.

The Identifier ( Entity ID) can be similar to https://yourdomain.com/

Reply URL : Specifies where the application expects to receive the SAML token. The reply URL is also referred to as the Assertion Consumer Service (ACS) URL. You can use the additional reply URL fields to specify multiple reply URLs. For example, you might need additional reply URLs for multiple subdomains. Or, for testing purposes you can specify multiple reply URLs (local host and public URLs) at one time.

If you are using SimpleSAMLphp, the reply URL should be similar to https://<domain_name>/app/module.php/saml/sp/metadata.php/default-sp


