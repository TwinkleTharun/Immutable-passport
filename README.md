# Immutable-passport
Certainly, here's a complete guide for integrating Immutable Passport into an application, including the necessary code examples.

---

# Immutable Passport Integration Guide

This guide will walk you through integrating Immutable Passport into your application. Immutable Passport is a secure and efficient way to authenticate users and perform blockchain transactions. We'll create a simple application to demonstrate the integration.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Creating a Simple Application](#creating-a-simple-application)
3. [Registering the Application on Immutable Developer Hub](#registering-the-application)
4. [Installing and Initializing the Passport Client](#installing-and-initializing-passport)
5. [Logging in a User with Passport](#logging-in-a-user)
6. [Displaying User Information](#displaying-user-information)
7. [Logging Out a User](#logging-out-a-user)
8. [Initiating a Transaction from Passport](#initiating-transaction)
9. [Conclusion](#conclusion)

## 1. Prerequisites
Before you start, make sure you have the following:

- Node.js installed on your machine.
- A basic understanding of JavaScript.
- An Immutable Developer Hub account.

## 2. Creating a Simple Application
You can start by creating a basic application using your preferred framework (e.g., React, Angular, or Vue). Here's a simple example using React:

```bash
npx create-react-app passport-demo
cd passport-demo
```

## 3. Registering the Application on Immutable Developer Hub
Go to the Immutable Developer Hub and create a new client and necessary details. This will provide you with the necessary client ID and client secret for Passport integration.
###Things to note when adding a client in the Developer Hub
There are a few crucial details that must be provided when adding a client:
Application Type: The type of your application. At the moment only the Web Application option is available. A Native option for mobile or desktop applications is coming soon.
Client name: The name you wish to use to identify your application.
Logout URLs: The URL that your users will be redirected to upon logging out of your application.
Callback URLs: The URL that your users will be redirected to once the authentication is complete. This is also where your application process the authentication response.
Web Origins URLs: The URLs that are allowed to request authorisation. This field is available when you select the Native application type.

## 4. Installing and Initializing the Passport Client
###Install the Immutable SDK
Run the following command in your project root directory.
```bash
npm install -D @imtbl/sdk
```

###Initialise Passport
Next, we'll need to initialise the Passport client. The Passport constructor accepts a PassportModuleConfiguration object, which will be like following sample code snippet:

```javascript
import { config, passport } from "@imtbl/sdk";
import { ethers } from "ethers";

const passportConfig = {
  clientId: process.env.IMMUTABLE_CLIENT_ID as string,
  redirectUri: "http://localhost:3000/callback",
  logoutRedirectUri: "http://localhost:3000/",
  scope: "transact openid offline_access email",
  audience: "platform_api",
  baseConfig: new config.ImmutableConfiguration({
    environment: config.Environment.SANDBOX, // Set the appropriate environment value
    apiKey: "", // Provide the apiKey if required
  }),
};
const passportInstance = new passport.Passport(passportConfig);
const passportProvider = passportInstance.connectEvm();
```

## 5. Logging in a User with Passport
To log in a user, use the following sample code:

```javascript
import { passportProvider, fetchAuth } from "@/lib/immutable";

const fetchAuth = async () => {
  try {
    const accounts = await passportProvider.request({
      method: "eth_requestAccounts",
    });
    console.log("Connected");
    console.log(accounts);
  } catch (error) {
    console.log(error);
  }
};
```

## 6. Displaying User Information
After successful login, you can access user information like the ID token, access token. Have a look on sample code:

```javascript
import { passportInstance } from "@/lib/immutable";

const fetchUser = async () => {
  try {
    const userProfile = await passportInstance.getUserInfo();
    const accessToken = await passportInstance.getAccessToken();
    const idToken = await passportInstance.getIdToken();

    // Display user information on your app
  } catch (error) {
    console.log(error);
  }
};
```

## 7. Logging Out a User
To log out a user, simply use the following code:

```javascript
import { passportInstance } from "@/lib/immutable";

const handleLogout = () => {
  passportInstance.logout();
};
```

## 8. Initiating a Transaction from Passport
To initiate a blockchain transaction, use the Passport client's transaction data as per following code:

```javascript
import { passportProvider, initiateTransaction } from "@/lib/immutable";

const handleTransaction = async (data) => {
  try {
    const transactionHash = await initiateTransaction({ data });
    // Handle the transaction response
  } catch (error) {
    console.error(error);
  }
};
```

## 9. Conclusion
You've successfully integrated Immutable Passport into your application. You can explore additional features and customize your application further using the Immutable Passport documentation.

For a fully detailed guide, simply visit: https://docs.immutable.com/docs/zkEVM/products/passport
