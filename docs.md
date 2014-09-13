#Introduction
The simTRAC API can be communicated with via JSON-RPC 2 over HTTPS. Authentication is handled via OAuth 1.0.

#Access Points
The simTRAC API has one main access point: `https://login.sitmrac.com.au/api/`

And additional access points for applications using 'User Token Access' / '3 Legged' Open Authentication:

##Request Token
`https://login.sitmrac.com.au/api/oauth/request_token.php`

##Authorization
`https://login.sitmrac.com.au/authorisation/oauth/authorise.php`

##Access Token
`https://login.sitmrac.com.au/api/oauth/access_token.php`


#Methods

`simtrac.test(any arg): string`
Returns a string representation of `arg`

`simtrac.get_token_ttl(string accessTokenKey): int`
Tests the current access token for time-to-live

`simtrac.get_user_details(): UserDetailsResponse`

Returns details on the current user
```js
UserDetailsResponse = {
  name_first: string, 
  name_last: string, 
  timezone: string, 
  email_address: string
}
```

`simtrac.get_vehicle(): GetVehiclesResponse`
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

