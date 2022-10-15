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
doc configuration for apache and nginx link :
https://simplesamlphp.org/docs/1.17/simplesamlphp-install.html
instructions found below:
https://www.lewisroberts.com/2015/09/05/single-sign-on-to-azure-ad-using-simplesamlphp/

step 1. setup SAML Azure AD SSO for your PHP web application using SimpleSAMLphp
In the app registrations in Azure AD, select your app and click on endpoints. Copy the Federation metadata document. The federation metadata should be imported to your application.

The Identifier, Reply URL and Sign on URL should be configured in the Azure AD.

Identifier (Entity ID) : Enter a URL that uses the following pattern: 'https://.yourdomain.com' You can find this value as the Issuer element in the AuthnRequest (SAML request) sent by the application.

The Identifier ( Entity ID) can be similar to https://yourdomain.com/

Reply URL : The reply URL is also referred to as the Assertion Consumer Service (ACS) URL. Specifies where the application expects to receive the SAML token. 
You can use the additional reply URL fields to specify multiple reply URLs. For example, you might need additional reply URLs for multiple subdomains. Or, for testing purposes you can specify multiple reply URLs (local host and public URLs) at one time.

If you are using SimpleSAMLphp, the reply URL should be similar to https://<domain_name>/app/module.php/saml/sp/metadata.php/default-sp

step 2. save the metadata from azure
step 3. open simplesamlphp web interface , visit federation tab and use the tool 'XML to simplesaml metadata converter'
step 4. copy the converted content to the folder 'metadata' under simplesamlphp - eg: save it as saml20-idp-remote.php
step 5 . open config folder -> authsources.php
edit the commented section  
default-sp - 
 - change the entityID value to reflect the name or URL of your app domain
 - idp value , which is the first line of the converted metadata actually gives you the IdP (Identity Provider) – in this case, Azure AD.
 - discoURL is null (stays same)
 - add these two lines below discoURL
 'NameIDFormat' => 'urn:oasis:names:tc:SAML:2.0:nameid-format:persistent',
'simplesaml.nameidattribute' => 'eduPersonTargetedID',
- save the authsources.php and close the file
step 6: test the auth using provided authentication tab 
use the link - default-sp
step 7: likely will receive on error on the test page
take the Reply URL and add to azure
In the Azure Management portal, find the application, scroll to Single Sign-On and add it to the list of Reply URLs.
and save
step 8: test again and it should work, will be shown  the azure microsoftonline Sign in page
step 9: you will be redirected to SimpleSAMLphp
step 10: strictly recommended to change config.php - for... add salt, admin password change for simplesaml gui , enable modules, email notifications, 



