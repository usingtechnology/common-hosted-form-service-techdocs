[Home](.) > [Developer](Developer) > **Developer Additional Resources**
***

# Common Services API Access
**[Back to top](#top)**

This service requires an IDIR account. You can open this link https://api.gov.bc.ca/devportal/api-directory to request an account after logging in as a developer with your IDIR. This will provide you with an API client id and secret to the CHES and CDOGS service.

[CDOGS](https://api.gov.bc.ca/devportal/api-directory/3181?preview=false)

[CHES](https://api.gov.bc.ca/devportal/api-directory/3182?preview=false)

It’s not necessary to immediately obtain access to CHES and CDOGS. If you wanted to take advantage of the document generator and email service in the future then this is where you would do it.

***

# 403 Error
**[Back to top](#top)**

Accessing CHEFS from an external network may result in a forbidden access 403 Error. To fix this, navigate to the Keycloak login page at http://localhost:8082/ and log in with the username and password “admin” after you have completed the build process. Under `Configure > Clients`, for both `chefs` and `chefs-backend`, add an asterisk `*` to the `Web Origins` field. This will permit all CORS origins and should solve the 403 Forbidden Error. 

***

# Using Test Installation JSON
**[Back to top](#top)**

By default, the build files are set up to support the ‘Development’ Installation JSON from the [Common Hosted Single Sign-On (CSS)](https://bcgov.github.io/sso-requests) page. If you wish to use the ‘Test’ Installation JSON, navigate to http://localhost:8082/ and login to your Keycloak Administration Console. Under `Configure > Identity Providers`, change all the **https://dev.loginproxy.gov.bc.ca** URL’s to **https://test.loginproxy.gov.bc.ca**. 

This can be accomplished as a more permanent solution by changing all the URL’s in `realm-export.json` from **https://dev.loginproxy.gov.bc.ca** to **https://test.loginproxy.gov.bc.ca**. If already built, this process will require you to delete the Docker containers and volumes, and rebuild CHEFS. 

***
# Cannot Connect to the Docker Daemon
**[Back to top](#top)**  

Before running `docker compose`, you will need to start the Docker daemon.  
## Docker Desktop App  
Most Linux distributions use `systemctl` to start services.  Use the command `sudo systemctl start docker` to run the Docker daemon.  This command can be run in any folder using the command line program of your choice.
If you are using the Docker desktop app, starting the application and then running `docker compose up` will also work. 

## MacOS Ventura
Starting services in MacOS requires the `launchctl` command. Use the command `sudo launchctl start docker` to run the Docker daemon.   This command can be run in any folder using the command line program of your choice.  
If you are using MacOS Ventura and using launchctl or starting the docker daemon doesn't help with running docker compose up, then try the following:   
1. Open Docker Desktop  
2. go to Docker Engine  
3. Click on "Apply and Restart" (This will apply the json configurations)  

> Source documentation for [Docker Engine](https://docs.docker.com/desktop/settings/mac/#docker-engine).

***

# Localhost Port
**[Back to top](#top)**

If your system cannot run on the default port http://localhost:8081/, navigate to the Keycloak login page at http://localhost:8082/ and log in with the username and password “admin” after you have completed the build process. Under `Configure > Clients`, for both `chefs` and `chefs-backend`, add your URI under the `Valid Redirect URIs` field. 

***

For any other issues not covered on this page, kindly contact [Jason Chung](mailto:jason.chung@gov.bc.ca).