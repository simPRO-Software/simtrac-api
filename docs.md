#Introduction
The simTRAC API can be communicated with via JSON-RPC 2 over HTTPS. Authentication is handled via OAuth 1.0.

#Access Points
The simTRAC API has one main access point: `https://login.simtrac.com.au/api/`

And additional access points for applications using 'User Token Access' / '3 Legged' Open Authentication:

##Request Token
`https://login.simtrac.com.au/api/oauth/request_token.php`

##Authorization
`https://login.simtrac.com.au/authorisation/oauth/authorise.php`

##Access Token
`https://login.simtrac.com.au/api/oauth/access_token.php`


#Methods

`simtrac.test(any arg)` returns `string`

Returns a string representation of `arg`

`simtrac.get_token_ttl(string accessTokenKey)` returns `int`

Tests the current access token for time-to-live

`simtrac.get_user_details()` returns `UserDetailsResponse`

Returns details on the current user

```js
UserDetailsResponse = {
  name_first: string, 
  name_last: string, 
  timezone: string, 
  email_address: string
}
```

`simtrac.get_vehicle()` returns `GetVehiclesResponse`

Returns a list of vehicles accessible by the current users

```
GetVehiclesResponse = [
  {
     vehicle_id: int, 
     group_ids: [int], 
     vehicle_name: string, 
     registration_number: string,
     messaging: boolean,
     year_of_manufacture: string,
     make: string,
     imei: string,
     model: string,
     badge: string,
     body_shape: string,
     vin: string,
     engine_number: string,
     fuel: string
     notes: string
  }
]
```


`simtrac.get_group()` returns `GetGroupsResponse`

Returns a list of groups accessible by the current users

```
GetGroupsResponse = [
  {
    group_id: int,
    group_name: string,
    group_description: string
  }
]
```


`simtrac.get_drivers()` returns `GetDriversResponse`

Returns a list of drivers accessible by the current users

```
GetDriversResponse = [
  {
    driver_id: int,
    name_first: string,
    name_last: string,
    phone_mobile: string,
    phone_other: string,
    licence_no: string,
    licence_expiry: string,
    licence_class: string,
    notes: string
  }
]
```

`simtrac.get_vehicle_position([string since])` returns `GetVehiclePositionResponse`

Returns the current positions for vehicles; if they have been updated since `since`.

Pass the `retrieved` parameter back to the next call as `since`.

```
GetVehiclePositionResponse = {
  retrieved: string,
  vehicle_stats: [
    {
      vehicle_id: int,
      longitude: string,
      latitude: string,
      position_update: string,
      direction: int,
      speed: int,
      status_acc: boolean,
      driver_id: int,
      driver_name: string,
      invalid_count: int,
      last_status_change: string,
      status_change_interval: int,
      status_switch: int,
      current_address: string,
      message_count: int,
      geofences: [int],
      geosites: [int],
      last_activity: int
    }
  ]
}
```

`simtrac.send_message(int vehicle_id, string message)` returns `boolean`

Sends a message to the specified vehicle


`simtrac.get_messages_inbox([string since])` returns ` GetMessagesInboxResponse`

Returns the current inbox messages; if they have been updated since `since`.

Pass the `retrieved` parameter back to the next call as `since`.

```
GetMessagesInboxResponse = {
  retrieved: string,
  messages: [
    {
      vehicle_message_received_id: int,
      vehicle_id: int,
      vehicle_name: string,
      driver_name: string,
      datetime: string,
      message: string,
      message_read: boolean,
      archived: boolean
    }
  ]
}
```

`simtrac.get_messages_outbox([string since])` returns `GetMessagesOutboxResponse`

Returns the current outbox messages; if they have been updated since `since`.

Pass the `retrieved` parameter back to the next call as `since`.

```
GetMessagesOutboxResponse = {
  retrieved: string,
  messages: [
    {
      vehicle_message_sent_id: int,
      vehicle_id: int,
      vehicle_name: string,
      driver_name: string,
      user_id: int,
      name_first: string,
      name_last: string,
      date_created: string,
      message: string,
      sent: string,
      delivered: string,
      archived: boolean,
      latlng: string,
      location_address: string,
      message_response: string,
      message_status: string
    }
  ]
}
```


`simtrac.set_message_read(int message_received_id)` returns `boolean`

Marks a received message as read


`simtrac.set_message_unread(int message_received_id)` returns `boolean`

Marks a received message as unread


`simtrac.set_message_archived(int message_sent_id)` returns `boolean`

Archives a sent message

`simtrac.set_message_unarchived(int message_sent_id)` returns `boolean`

Un-archives a sent message
