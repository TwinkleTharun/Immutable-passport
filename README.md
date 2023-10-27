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
Next, we'll need to initialise the Passport client. The Passport constructor accepts a PassportModuleConfiguration object, which has the following interface:

```javascript
interface PassportModuleConfiguration {
  baseConfig: ImmutableConfiguration;
  clientId: string;
  logoutRedirectUri: string;
  logoutMode?: 'redirect' | 'silent'; // defaults to 'redirect'
  redirectUri: string;
  scope?: string;
  audience?: string;
}
```

## 5. Logging in a User with Passport
Create a login button in your application. When the user clicks it, use the `passport.login()` method to initiate the Passport authentication flow:

```javascript
passport.login().then((result) => {
  if (result) {
    // User is logged in, you can perform actions here.
  }
});
```

## 6. Displaying User Information
After successful login, you can access user information like the ID token, access token, and nickname:

```javascript
const idToken = passport.getIdToken();
const accessToken = passport.getAccessToken();
const nickname = passport.getNickname();

console.log('ID Token:', idToken);
console.log('Access Token:', accessToken);
console.log('Nickname:', nickname);
```

## 7. Logging Out a User
To log out a user, simply call the `passport.logout()` method:

```javascript
passport.logout();
```

## 8. Initiating a Transaction from Passport
To initiate a blockchain transaction, use the Passport client's `initiateTransaction()` method:

```javascript
passport.initiateTransaction({ data: 'Your transaction data' }).then((transactionHash) => {
  console.log('Transaction Hash:', transactionHash);
});
```

## 9. Conclusion
You've successfully integrated Immutable Passport into your application. You can explore additional features and customize your application further using the Immutable Passport documentation.

For a fully detailed guide and a sample React application demonstrating the integration, take a look of source files in the repository.
