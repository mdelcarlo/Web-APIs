# PublicKeyCredential
The PublicKeyCredential interface provides information about a public key / private key pair, which is a credential for logging in to a service using an un-phishable and data-breach resistant asymmetric key pair instead of a password. It inherits from Credential, and was created by the Web Authentication API extension to the Credential Management API. Other interfaces that inherit from Credential are PasswordCredential and FederatedCredential.

## Properties
#### PublicKeyCredential.type |  Read only | Secure context
Inherited from Credential. Always set to public-key for PublicKeyCredential instances.
#### PublicKeyCredential.id |  Read only | Secure context
Inherited from Credential and overridden to be the base64url encoding of #### PublicKeyCredential.rawId.
#### PublicKeyCredential.rawId |  Read only | Secure context
An ArrayBuffer that holds the globally unique identifier for this #### PublicKeyCredential. This identifier can be used to look up credentials for future calls to CredentialsContainer.get.
#### PublicKeyCredential.response |  Read only  | Secure context
An instance of an AuthenticatorResponse object. It is either of type AuthenticatorAttestationResponse if the PublicKeyCredential was the results of a navigator.credentials.create() call, or of type AuthenticatorAssertionResponse if the PublicKeyCredential was the result of a navigator.credentials.get() call.
## Methods
#### PublicKeyCredential.getClientExtensionResults() | Secure context
If any extensions were requested, this method will return the results of processing those extensions.
#### PublicKeyCredential.isUserVerifyingPlatformAuthenticatorAvailable() | Secure context
A static method returning a Promise which resolves to true if an authenticator bound to the platform is capable of verifying the user. With the current state of implementation, this method only resolves to true when Windows Hello is available on the system.

## Examples
#### Creating a new instance of PublicKeyCredential
Here, we use navigator.credentials.create() to generate a new credential.

```js
var publicKey = {
  challenge: /* from the server */,
  rp: {
    name: "Example CORP",
    id  : "login.example.com"
  },
  user: {
    id: new Uint8Array(16),
    name: "jdoe@example.com",
    displayName: "John Doe"
  },
  pubKeyCredParams: [
    {
      type: "public-key",
      alg: -7
    }
  ]
};

navigator.credentials.create({ publicKey })
  .then(function (newCredentialInfo) {
    var response = newCredentialInfo.response;
    var clientExtensionsResults = newCredentialInfo.getClientExtensionResults();
  }).catch(function (err) {
     console.error(err);
  });
  ```
#### Getting an existing instance of PublicKeyCredential
Here, we fetch an existing credential from an authenticator, using navigator.credentials.get().
```js
var options = {
  challenge: new Uint8Array([/* bytes sent from the server */])
};

navigator.credentials.get({ "publicKey": options })
    .then(function (credentialInfoAssertion) {
    // send assertion response back to the server
    // to proceed with the control of the credential
}).catch(function (err) {
     console.error(err);
});
```