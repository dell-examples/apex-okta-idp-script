# Dell APEX API auth token script
- This is a sample script being given out to the customers to be able to fetch the auth token to call APEX public APIs.
- The script fetches the SAML token by using IdP initiated SSO, and uses this SAML token along with the client id/script that the customer created via the APEX console, to exchange for a Access token which is used to call the APEX public APIs.
- This script currently supports Okta and Azure Entra IdP.
- Customers should be able to change this script according to their needs as the IdP configurations for different customers could be any number of combinations

The following procedures cover how to, first, configure the configuration file used by the script, with information from your IdP
and, second, run the provided script to retrieve a token.

The requirements.txt file lists the libraries that the script depends on.

# Get a Dell Identity JSON web token using Okta IDP

##Configure config.json:

To get a Dell APEX JSON web token, you will first need to retrieve information specific to Okta IDP and then input that information into the config.json file.

Follow this procedure to configure the config.json file with the following information from Okta IDP:
```shell
   - SAML endpoint
   - Login endpoint
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

## Retrieve token:

1. If this is the first time you are running the script, install all the dependencies first by running the following:
```console
pip install -r requirements.txt
```
2. Run the saml_get_token.py file and select 'Okta' as the desired IdP.
```
python saml_get_token.py
```
2. Review the IdP URL configurations.
   If you choose to update the configurations, re-run the saml_get_token.py file.
```shell
  - You can also update IdP URL configurations in the config.json file.
```
3. Enter credentials for the IdP.
4. Enter your access key ID and secret.

You will receive a Dell Identity JSON web token that can be used to make requests to the Dell APEX Navigator for Multicloud Storage API.

The Dell Identity JSON web token expires after 30 minutes and cannot be renewed. To make further calls, generate a new token with an access key, secret, and SAML token.

# Get a Dell Identity JSON web token using Azure Entra IDP

## Configure config-entra.json:
To get a Dell APEX JSON web token, you will first need to retrieve information specific to Azure Entra IDP and then input that information into the config-entra.json file.
Update the config-entra.json by setting the saml_endpoint, username, password, saml_pipe, assertion_consumer_service_url, and entra_app_client_secret according to the directions in the config-entra.json.


## Retrieve token:
1. If this is the first time you are running the script, install all the dependencies first by running the following:
```console
pip install -r requirements.txt
```
2. Then, run
```
python saml_get_entra_token.py
```