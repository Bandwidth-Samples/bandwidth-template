# Repo Title REPLACE
<a href="http://dev.bandwidth.com"><img src="https://s3.amazonaws.com/bwdemos/BW-VMP.png"/></a>
</div>

 # Table of Contents

<!-- TOC -->

- [Repo Title REPLACE](#repo-title-replace)
- [Bandwidth](#bandwidth)
- [Environmental Variables](#environmental-variables)
- [Callback URLs](#callback-urls)
    - [Ngrok](#ngrok)

<!-- /TOC -->

# Bandwidth

In order to use the Bandwidth API users need to set up the appropriate application at the [Bandwidth Dashboard](https://dashboard.bandwidth.com/) and create API tokens.

To create an application log into the [Bandwidth Dashboard](https://dashboard.bandwidth.com/) and got to the `Applications` tab.  Fill out the **New Application** form selecting the service (Messaging or Voice) that the application will be used for.  All Bandwidth services require publicly accessible Callback URLs, for more information on how to set one up see [Callback URLs](#callback-urls).

More information about API credentials can be found [here](https://dev.bandwidth.com/guides/accountCredentials.html#top)

# Environmental Variables
The sample app uses the below environmental variables.
```java
BANDWIDTH_ACCOUNT_ID       // Your Bandwidth Account Id
BANDWIDTH_APPLICATION_ID   // Your Application Id created in the dashboard
BANDWIDTH_USERNAME         // Your Bandwidth API Token
BANDWIDTH_PASSWORD         // Your Bandwidth API Secret
BANDWIDTH_PHONENUMBER      // Your The Bandwidth Phone Number
```

# Callback URLs

For a detailed introduction to Bandwidth Callbacks see https://dev.bandwidth.com/guides/callbacks/callbacks.html 

## Ngrok

A simple way to set up a callback URL is to use the tool [ngrok](https://ngrok.com/).  
After you have downloaded and installed `ngrok` run the following command to open a public tunnel to port 8080
```cmd
ngrok http 8080
```
You can view your public URL at http://127.0.0.1:4040 after ngrok is running.  You can also view the status of the tunnel and requests/responses here.







