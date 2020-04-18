# Password Credential
The interface of the Credential Management API provides information about a username/password pair. In supporting browsers an instance of this class may be passed in the credential member of the init object for global fetch.

## Constructor
#### PasswordCredential() | Secure context
Creates a new PasswordCredential object.

## Properties
Inherits properties from its ancestor, Credential.

#### PasswordCredential.additionalData  | Secure context
One of a FormData instance, a URLSearchParams instance, or null. The data in the objects will be added to the request body and sent to the remote endpoint with the credentials.
#### PasswordCredential.iconURL Read only | Secure context
A USVString containing a URL pointing to an image for an icon. This image is intended for display in a credential chooser. The URL must be accessible without authentication.
#### PasswordCredential.idName |  Secure context
A USVString containing the name that will be used for the ID field when submitting the current object to a remote endpoint via fetch. This property defaults to 'username', but may be overridden to match whatever the backend service expects.
#### PasswordCredential.name Read only | Secure context
A USVString containing a human-readable public name for display in a credential chooser.
#### PasswordCredential.password Read only | Secure context
A USVString containing the password of the credential.
#### PasswordCredential.passwordName  | Secure context
A USVString representing the name that will be used for the password field when submitting the current object to a remote endpoint via fetch. This property defaults to 'password', but may be overridden to match whatever the backend service expects.

## Examples
#### Create a PasswordCredential
```js
var cred = new PasswordCredential({
  id: id,
  password: password,
  name: name,
  iconURL: iconUrl
});

navigator.credentials.store(cred)
 .then(function() {
 // Do something else.
})
```