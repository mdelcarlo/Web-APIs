# FederatedCredential 
The FederatedCredential interface of the the Credential Management API provides information about credentials from a federated identity provider. A federated identity provider is an entity that a website trusts to correctly authenticate a user, and that provides an API for that purpose. OpenID Connect is an example of a federated identity provider framework.

In browsers that support it, an instance of this interface may be passed in the credential member of the init object for global fetch.

## Constructor
#### FederatedCredential()
Creates a new FederatedCredential object.
## Properties
Inherits properties from its ancestor, Credential.

#### FederatedCredential.provider | Read only
Returns a USVString containing a credential's federated identity provider.
#### FederatedCredential.protocol | Read only
Returns a DOMString containing a credential's federated identity protocol.

## Examples
#### Generate and store a federated credential

```js
var credential = new FederatedCredential({
  id: 'delca',
  name: 'matias',
  provider: 'https://account.google.com',
});

// Store it
navigator.credentials.store(credential)
  .then(function(e) {    
    console.log(e)
});
```