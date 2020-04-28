# Encrypted Media Extensions
The Encrypted Media Extensions API provides interfaces for controlling the playback of content which is subject to a digital restrictions management scheme.

## Interfaces
### MediaKeyMessageEvent
Contains the content and related data when the content decryption module (CDM) generates a message for the session.
### MediaKeys
Represents a set of keys that an associated HTMLMediaElement can use for decryption of media data during playback.
### MediaKeySession
Represents a context for message exchange with a content decryption module (CDM).
### MediaKeyStatusMap
Is a read-only map of media key statuses by key IDs. 
### MediaKeySystemAccess
Provides access to a Key System for decryption and/or a content protection provider.
### MediaKeySystemConfiguration
Provides configuration information about the media key system.