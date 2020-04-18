# Credential Management
The Credential Management API lets a website store and retrieve user, federated, and public key credentials. These capabilities allow users to sign in without typing passwords, see the federated account they used to sign in to a site, and resume a session without the explicit sign-in flow of an expired session.

Interfaces
Credential
Provides information about an entity as a prerequisite to a trust decision.
CredentialsContainer
Exposes methods to request credentials and notify the user agent when interesting events occur such as successful sign in or sign out. This interfaces is accessible from navigator.credentials.
FederatedCredential
Provides information about credentials from a federated identity provider, which is an entity that a website trusts to correctly authenticate a user, and which provides an API for that purpose. OpenID Connect is an example of such a framework.
PasswordCredential
Provides information about a username/password pair.
PublicKeyCredential
Provides a credential for logging in using an un-phishable and data-breach resistant asymmetric key pair instead of a password.

## Concepts
This API lets websites interact with a user agent’s password system so that websites can deal in a uniform way with site credentials and user agents can provide better assistance with the management of their credentials. For example, user agents have a particularly hard time dealing with federated identity providers or esoteric sign-in mechanisms that use more than just a username and password. To address these problems, the Credential Management API provides ways for a website to store and retrieve different types of credentials. This give users capabilities such as seeing the federated account they used to sign on to a site, or resuming a session without the explicit sign-in flow of an expired session.

## Interfaces
### [Credential](./Credential/README.md)
Provides information about an entity as a prerequisite to a trust decision.

### CredentialsContainer
Exposes methods to request credentials and notify the user agent when interesting events occur such as successful sign in or sign out. This interfaces is accessible from navigator.credentials.

### [FederatedCredential](./FederatedCredential/README.md)

Provides information about credentials from a federated identity provider, which is an entity that a website trusts to correctly authenticate a user, and which provides an API for that purpose. OpenID Connect is an example of such a framework.

### [PasswordCredential](./PasswordCredential/README.md)

Provides information about a username/password pair.

### [PublicKeyCredential](./PublicKeyCredential/README.md)


Provides a credential for logging in using an un-phishable and data-breach resistant asymmetric key pair instead of a password.