# apex-okta-idp-script
- This is a sample script being given out to the customers to be able to fetch the access token to call APEX public APIs.
- The script fetches the SAML token by using IdP initiated SSO, and uses this SAML token along with the client id/script that the customer created via the APEX console, to exchange for a Access token which is used to call the APEX public APIs.
- This script currently supports Okta IdP.
- Customers should be able to change this script according to their needs as the IdP configurations for different customers could be any number of combinations

# Get a Dell Identity JSON web token
The following procedures cover how to, first, configure the config.json file with information from your IdP and, second, run the provided script to retrieve a token.

The requirements.txt file lists the libraries that the script depends on.
Install those dependencies from the command line by running the following:
pip install -r requirements.txt
# Configure config.json:

To get a Dell APEX web token, you will first need to retrieve information specific to your IdP and then input that information into the config.json file.

The following procedures describe how to find each service's information:

# Okta:

 Follow this procedure to configure the config.json file with the following information from Okta:
```shell
   - SAML endpoint
   - login endpoint
```
1. In a browser, navigate to Okta and copy your login URL.
2. In the config.json file, paste the URL as the value for saml_endpoint.
   This is the first half of your SAML endpoint.
3. Log into Okta.
4. Right click and copy the SSO application URL.
5. In the config.json file, paste the URL as the value for login_endpoint.
6. Open the command line and run the following command:
```shell
   curl -v -L https://{login_endpoint} 2>&1 > /dev/null | grep GET
```
7. In the output, copy the path in the second GET request.
8. In the config.json file, append the path to the value for saml_endpoint.
   This is the second half of your SAML endpoint.
9. Save the changes made to the config.json file and proceed to the next section

Retrieve token:

To get a Dell Identity JSON web token:

1. Run the saml_get_token.py file and select the desired IdP.
2. Review the IdP URL configurations.
   If you choose to update the configurations, re-run the saml_get_token.py file.
```shell
  - You can also update IdP URL configurations in the config.json file.
```
3. Enter credentials for the IdP.
4. Enter your access key ID and secret.

You will receive a Dell Identity JSON web token that can be used to make requests to the Dell APEX Navigator for Multicloud Storage API.

The Dell Identity JSON web token expires after 30 minutes and cannot be renewed. To make further calls, generate a new token with an access key, secret, and SAML token.