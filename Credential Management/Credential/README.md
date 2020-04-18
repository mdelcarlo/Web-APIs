# Credential 
The Credential interface of the the Credential Management API provides information about an entity as a prerequisite to a trust decision.

## Properties
#### Credential.id | Read only
Returns a DOMString containing the credential's identifier. This might be any one of a GUID, username, or email address.
#### Credential.type | Read only
Returns a DOMString containing the credential's type. Valid values are password, federated and public-key. (For PasswordCredential, FederatedCredential and PublicKeyCredential)