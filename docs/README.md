# Message Flow

## Table of Contents

- [Context](#context)
- [Services](#services)
  - [User Service](#user-service)
- [Channels](#channels)
  - [notification.preferences.update](#notificationpreferencesupdate)
  - [user.analytics](#useranalytics)
  - [user.info.request](#userinforequest)
  - [user.info.update](#userinfoupdate)

## Context

![Context](diagrams/context.svg)

## Services

### User Service

A service that manages user information, profiles, and authentication.
Handles user data requests, profile updates, and user lifecycle events.


![User Service Service Channels](diagrams/service_user-service.svg)

## Channels

### notification.preferences.update

![notification.preferences.update Channel Services](diagrams/channel_notificationpreferencesupdate.svg)

#### Messages
**PreferencesUpdateMessage**
```json
{
  "preferences": {
    "categories": {
      "marketing": "boolean",
      "security": "boolean",
      "updates": "boolean"
    },
    "email_enabled": "boolean",
    "push_enabled": "boolean",
    "quiet_hours": {
      "enabled": "boolean",
      "end": "string[time]",
      "start": "string[time]"
    },
    "sms_enabled": "boolean"
  },
  "updated_at": "string[date-time]",
  "user_id": "string[uuid]"
}
```

### user.analytics

![user.analytics Channel Services](diagrams/channel_useranalytics.svg)

#### Messages
**UserAnalyticsEventMessage**
```json
{
  "event_id": "string[uuid]",
  "event_type": "string[enum:user_registered,user_logged_in,profile_updated,preferences_changed,account_deleted]",
  "metadata": {
    "environment": "string[enum:development,staging,production]",
    "platform": "string[enum:ios,android,web]",
    "source": "string[enum:mobile,web,api]",
    "version": "string"
  },
  "timestamp": "string[date-time]",
  "user_id": "string[uuid]"
}
```

### user.info.request

![user.info.request Channel Services](diagrams/channel_userinforequest.svg)

#### Messages
**request**: UserInfoRequestMessage
```json
{
  "user_id": "string[uuid]"
}
```
**reply**: UserInfoReplyMessage
```json
{
  "email": "string[email]",
  "error": {
    "code": "string",
    "message": "string"
  },
  "language": "string",
  "name": "string",
  "timezone": "string",
  "user_id": "string[uuid]"
}
```

### user.info.update

![user.info.update Channel Services](diagrams/channel_userinfoupdate.svg)

#### Messages
**UserInfoUpdateMessage**
```json
{
  "changes": "object",
  "metadata": {
    "environment": "string[enum:development,staging,production]",
    "platform": "string[enum:ios,android,web]",
    "source": "string[enum:mobile,web,api]",
    "version": "string"
  },
  "updated_at": "string[date-time]",
  "user_id": "string[uuid]"
}
```
