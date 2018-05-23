# User

The API allows you to create, delete, and update your users with addition of social providers and passwordless authentication using magic link. You can retrieve individual users as well as a list of all your users. Also the api gives ability to set authorization level privileges using the rules object.

## Signup using email and password

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signup"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
  -d '{
       "email":"test", 
       "password":"test@#987"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
    "email": "test@mail.com",
    "rules": [],
    "groups": [],
    "meta": "",
    "devicetokens": [
        {
            "token": "KHE-PdB5YpsUPYnudAzRMflS1n-gDzgvOgGSa5jvEKYRlirNtQ76Vurvq2GsM3FnmGdno7eKBltB0T047mbgKg==",
            "deviceid": "test_56789657567"
        }
    ],
    "verified": false,
    "createdAt": "2018-03-22T14:12:14.780714+05:30",
    "updatedAt": "2018-03-22T14:12:14.780716+05:30"
}
```

Creates a new user object.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signup</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
email | required | string | The email address to send the verfication. 
password | required | string | The password to set for the user to authenticate. 

### Returns

Returns a user object if correct email and password was provided. The returned object will have information about the rules, groups, metadata. If no email or password was provided, same email which already exists or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Either email or password is missing`
3.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Email is not valid`
4.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Password must be atleast 7 characters long`
5.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `You are already registered with product1 and product2`
6.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## SignIn using github


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/github"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
    "redirectUrl": "https://github.com/login/oauth/authorize?access_type=online&approval_prompt=auto&client_id=2857b5e2c2a665741368&redirect_uri=http%3A%2F%2Fa2c77437.ngrok.io%2Fv1%2Fcallback%2Fgithub&response_type=code&scope=user&state=eyJib2R5Ijoie1xuXHRcIm1ldGFcIjpcInVwZGF0ZWQgYXBpIG1ldGFcIlxufSIsInByb2R1Y3RUb2tlbiI6IjF5NHkydmE4dmZaNGoxQ2kxcXZHcmVRLXU4T3dEM0xqWVE5a3NlZ3hFcDA9In0%3D_a50b822630358ec4b16cc66f8e7d51c9508f3ed1"
}

```

Creates a new user object via github.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/github</code>

### Returns

Returns a redirect url. The redirect url will be used to authenticate the user using github. If the user is successfully authenticated using github, goodcop will redirect to the product callback. If no callback is set by the product, social auth provider failure or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Callback is set for your product, please set that first`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## SignIn using facebook


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/google"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
    "redirectUrl": "https://accounts.google.com/o/oauth2/auth?access_type=online&approval_prompt=auto&client_id=581118883872-dgnlvtv9l8h3j0m7nipgtcoot3rgcc41.apps.googleusercontent.com&redirect_uri=http%3A%2F%2Fa2c77437.ngrok.io%2Fv1%2Fcallback%2Fgoogle&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.profile&state=eyJib2R5Ijoie1xuXHRcIm1ldGFcIjpcInVwZGF0ZWQgYXBpIG1ldGFcIlxufSIsInByb2R1Y3RUb2tlbiI6IjF5NHkydmE4dmZaNGoxQ2kxcXZHcmVRLXU4T3dEM0xqWVE5a3NlZ3hFcDA9In0%3D_a50b822630358ec4b16cc66f8e7d51c9508f3ed1"
}

```

Creates a new user object via google.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/google</code>

### Returns

Returns a redirect url. The redirect url will be used to authenticate the user using google. If the user is successfully authenticated using google, goodcop will redirect to the product callback. If no callback is set by the product, social auth provider failure or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Callback is set for your product, please set that first`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## SignIn using facebook


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/facebook"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
    "redirectUrl": "https://www.facebook.com/dialog/oauth?access_type=online&approval_prompt=auto&client_id=1715535545188089&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2Fv1%2Fcallback%2Ffacebook&response_type=code&scope=email&state=eyJib2R5Ijoie1xuXHRcImVtYWlsXCI6IFwidmFpYmhhdkBjbG91ZGNvdmVyLmluXCJcbn0iLCJkZXZpY2VJZCI6IiIsInByb2R1Y3RUb2tlbiI6IkdRU05VQWpFUTNnU19uVXl6NXhvSUwwVlh3ZG9EUnRyajBLNkI1blJQcjQ9IiwidXNlclRva2VuIjoiIn0%3D_b88554542246d0c1a092a16c66ec960f4972364d"
}

```

Creates a new user object via facebook.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/facebook</code>

### Returns

Returns a redirect url. The redirect url will be used to authenticate the user using facebook. If the user is successfully authenticated using facebook, goodcop will redirect to the product callback. If no callback is set by the product, social auth provider failure or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Callback is set for your product, please set that first`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## SignIn using twitter


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/twitter"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
    "redirectUrl": "https://api.twitter.com/oauth/authorize?oauth_token=a54r3gAAAAAA4-PrAAABYkvwDWA"
}

```

Creates a new user object via twitter.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/twitter</code>

### Returns

Returns a redirect url. The redirect url will be used to authenticate the user using twitter. If the user is successfully authenticated using twitter, goodcop will redirect to the product callback. If no callback is set by the product, social auth provider failure or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Callback is set for your product, please set that first`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## SignIn using instagram


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/instagram"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
    "redirectUrl": "https://api.instagram.com/oauth/authorize?access_type=online&approval_prompt=auto&client_id=71e9de2416cf498285fdce2414fcba79&redirect_uri=http%3A%2F%2F127.0.0.1%3A8080%2Fv1%2Fcallback%2Finstagram&response_type=code&scope=basic&state=eyJib2R5IjoiIiwiZGV2aWNlSWQiOiIiLCJwcm9kdWN0VG9rZW4iOiJHUVNOVUFqRVEzZ1NfblV5ejV4b0lMMFZYd2RvRFJ0cmowSzZCNW5SUHI0PSIsInVzZXJUb2tlbiI6IiJ9_17061fa5b0f196ab26b3ca2ca44259b4353a42dd"
}

```

Creates a new user object via instagram.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/instagram</code>

### Returns

Returns a redirect url. The redirect url will be used to authenticate the user using instagram. If the user is successfully authenticated using instagram, goodcop will redirect to the product callback. If no callback is set by the product, social auth provider failure or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Callback is set for your product, please set that first`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## SignIn using magiclink


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/magiclink"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
  -d '{
       "email":"some_email@mail.com", 
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "message": "Magic link sent to email successfully"
}

```

Creates a new user object via email by creating a token that will allow user to log in through the link sent to their email.


### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/magiclink</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
email | required | string | The email address to send the magic link to. 

### Returns

Returns a success message and an email will be sent to user with the magic link. Once user clicks on magic link goodcop will redirect to the product callback. If no email was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Email is missing`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## SignIn using phonenumber


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/phone"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
  -d '{
       "phoneNumber":"+917678788789", 
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json

{
	"message": "OTP sent to your mobile successfully"
}

```

Creates an one time password for user verfication.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/phone</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
phoneNumber | required | string | Phone number to send otp 

### Returns

Returns a success message and an one time password will be sent to user to verify.If no email was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Phone number is missing`
3.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `SMS sending error`
4.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Verfiy phonenumber

> Definition


> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/signin/phone/verify"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
  -d '{
       "phoneNumber":"+917678788789", 
       "otp":"878787"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
	"message": "to be updated"
}

```

Creates a new user object after verifying the otp.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/signin/phone/verify</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
phoneNumber | required | string | Phone number of the user 
otp | required | string | otp sent to user mobile

### Returns

Returns a user object if correct otp and phoneNumber was provided. The returned object will have user details with phone number and token. If no otp or phoneNumber was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Phone number or OTP missing`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Login

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/login"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json" \
  -H "Device-Token: test_56789657567"
  -d '{
       "email":"test", 
       "password":"test@#987"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
    "email": "test@mail.com",
    "rules": null,
    "groups": null,
    "meta": "",
    "devicetokens": [
        {
            "token": "R4QzpVxvYuS03W-ap54J6tgDj86pkGNQ60szc_7PbR1D4jbhJk1cFmJAjOUPpoew5vSV_prXFsRUxKeuY-GLxg==",
            "deviceid": "test_56789657567"
        }
    ],
    "verified": false,
    "createdAt": "2018-03-22T14:13:19.654089+05:30",
    "updatedAt": "2018-03-22T14:13:19.654091+05:30"
}

```

LogsIn the user.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/login</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
email | required | string | The email address of the user
password | required | string | The password of the user

### Returns

Returns a user object if correct email and password was provided. The returned object will have information about the rules, groups, metadata. If no email or password was provided, incorrect passowrd/email validation or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Either email or password is missing`
3.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Password must be atleast 7 characters long`
4.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `No Password,Please Set a password after signing in using magic link`
5.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Change password

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/passwordChange"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
  -H 'user-token: test_MLd587_Hi3TrTwfLNRg8mKiUwDlM7Z5VuODE9KhM8=' \
  -d '{
       "oldapassword":"test", 
       "newpassword":"test@#987"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
   "message":"Password Changed Successfully"
}
```

Change the password for the logged in user providing the oldpassword and new password.

### HTTPS Request

<code style="background:#4CAF50;">POST</code> <code style="background:#E8F5E9;">https://[GOODCOP_URL]/v1/user/passwordChange</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
oldapassword | required | string | The old password of the user. 
newapassword | required | string | The new password to set. 

### Returns

Returns a success message. If no user token was provided, incorrect passwords or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Wrong Old Password`
4.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Password must be atleast 7 characters long`
5.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## Get user by Id

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
    "email": "test@mail.com",
    "rules": null,
    "groups": null,
    "meta": "",
    "devicetokens": [
        {
            "token": "u82e715S5xutCVdu-EIL4A63g7Z_uFNLYAnrIjQbO10iYFiwkPher5BVqoin8hcHeFifSpcQ6x3hAx1CPigNbA==",
            "deviceid": "test_56789657567"
        }
    ],
    "verified": true,
    "createdAt": "0001-01-01T05:21:10+05:21",
    "updatedAt": "0001-01-01T05:21:10+05:21"
}
```

Retrieves the details of an existing user. You need only supply the unique user identifier that was returned upon user creation.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user/{userID}</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns a user object if a valid identifier was provided. If invalide user id was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Get user By email

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/getUser/test@mail.com"
  -X POST
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
    "email": "test@mail.com",
    "rules": null,
    "groups": null,
    "meta": "",
    "devicetokens": [
        {
            "token": "e_aMotSZFW0A9QiXWE0N2dkDIiLUBLHLrS6hAQyhD98Py11RAb4_YKjNijvaX4m5qWN8JwBhhi48iecFF38DmA==",
            "deviceid": ""
        }
    ],
    "verified": true,
    "createdAt": "2018-03-22T11:25:29.803822+05:30",
    "updatedAt": "2018-03-22T11:26:29.536281+05:30"
}
```

Retrieves the details of an existing user. You need only supply the unique email of the user.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/getUser/{email}</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
email | required | string | Valid email address 

### Returns

Returns a user object if a valid identifier was provided. If invalid email was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `Email is not valid`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## List all users

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "users": [
        {
            "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
            "email": "test@mail.tv",
            "rules": [
                {
                    "verb": "PUT",
                    "path": "/credentials/new/smart/5687539843203072",
                    "effect": true
                }
            ],
            "groups":  [
                5647053199769600,
                5687905720729600
            ],
            "meta": "",
            "devicetokens": [
                    {
                        "token": "e_aMotSZFW0A9QiXWE0N2dkDIiLUBLHLrS6hAQyhD98Py11RAb4_YKjNijvaX4m5qWN8JwBhhi48iecFF38DmA==",
                        "deviceid": ""
                    }
                ],
            "verified": false,
            "createdAt": "0001-01-01T05:21:10+05:21",
            "updatedAt": "2018-03-22T12:08:02.07777+05:30"
        },
        {
              "userId": "test1_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
              "email": "test1@mail.com",
              "rules": null,
              "groups": null,
              "meta": "",
               "devicetokens": [
                    {
                        "token": "TVzm6SDRY5i5lpXgrsNYxok9zgJODJsA7VB15yl2qvUeTG_n3HYmEHaYwt73K-1vGpsUTV18wssDyEWGHdInPw==",
                        "deviceid": "13ACFCFB-40F6-4823-B8FC-8CA3D3A5DEDE"
                    }
                ],
              "verified": true,
              "createdAt": "0001-01-01T05:21:10+05:21",
              "updatedAt": "2018-03-22T12:08:02.07777+05:30"
        },
    ]
}
```
Retrieves the detailed list of all product users. The users are returned in descending order of creation.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user</code>

### Returns

Returns a list of user objects. If any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`
2.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Delete user by Id

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "message": "User deleted successfully"
}

```

Deletes a user from the product. The user is not deleted permanently.

### HTTPS Request


<code style="background:#EF5350;">DELETE</code> <code style="background:#FFEBEE;">https://[GOODCOP_URL]/v1/user/{userID}</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns a message on success. If the user ID does not exist an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Get Group Details By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/groups"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
[
    {
        "groupId": 5717800035287040,
        "name": "CloudCover",
        "description": "",
        "rules": [
            {
                "verb": "PUT",
                "path": "/credentials/new/smart/5687539843203072",
                "effect": false
            },
            {
                "verb": "PUT",
                "path": "/credentials/new/smart/*",
                "effect": true
            }
        ],
        "meta": "",
        "productId": 5750501782061056
    },
    {
        "groupId": 5664530495438848,
        "name": "CloudCover|admin",
        "description": "",
        "rules": [
            {
                "verb": "PUT",
                "path": "/organizations/5717800035287040",
                "effect": true
            },
            {
                "verb": "PUT",
                "path": "/organizations/5664530495438848",
                "effect": true
            }
        ],
        "meta": "",
        "productId": 5750501782061056
    }
]
```

Retrieves the group details provided the user ID.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user/{userID}/groups</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns an array of group objects. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key` 
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## Get User Meta By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/meta"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "meta": "storing test meta info",
}
```
Retrieves the meta details provided the user ID.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user/{userID}/meta</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 


### Returns

Returns meta string. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`



## Update User Meta By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/meta"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
  -d '{
	"meta":"storing test meta info"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200 </code>

```json
{
    "userId": "test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a",
    "email": "test@mail.com",
    "rules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ],
    "groups": [
        5717800035287040,
        5664530495438848,
    ],
    "meta": "storing test meta info",
    "devicetokens": [
                    {
                        "token": "TVzm6SDRY5i5lpXgrsNYxok9zgJODJsA7VB15yl2qvUeTG_n3HYmEHaYwt73K-1vGpsUTV18wssDyEWGHdInPw==",
                        "deviceid": ""
                    }
    ],
    "verified": false,
    "createdAt": "0001-01-01T05:21:10+05:21",
    "updatedAt": "2018-03-22T12:08:02.07777+05:30"
}
```

Updates the meta by setting the value of the body parameter passed.

### HTTPS Request

<code style="background:#FFC107;">PUT</code> <code style="background:#FFF8E1;">https://[GOODCOP_URL]/v1/user/{userID}/meta</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
meta | required | string | Metadata to be stored for the user

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns user object with updated meta. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FFC107;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## List User Rules By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/rule"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "rules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "DELETE",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```

Retrieves the details of all user rules.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user/{userID}/rule</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns the list of user rules. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`

## Update User Rules By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/rule"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
  -d '[{
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
    }]'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "rules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "DELETE",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```

Updates the rules by setting the value of the body parameter passed.

### HTTPS Request

<code style="background:#FFC107;">PUT</code> <code style="background:#FFF8E1;">https://[GOODCOP_URL]/v1/user/{userID}/rule</code>

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
rules | required | array | rules to be updated 

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns updated rules. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## Delete User Rules By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/rule"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
  -d '[{
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
    }]'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "rules": [
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "DELETE",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```

Deletes the rules from the user.

### HTTPS Request

<code style="background:#EF5350;">DELETE</code> <code style="background:#FFEBEE;">https://[GOODCOP_URL]/v1/user/{userID}/rule</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns updated rules. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`


## Get Group Details for user By ID

> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/user/test_oio4205c7-4139-4e14-a0d0-c5932ad99e9a/groups"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
[
    {
        "groupId": 5198802495471616,
        "name": "admin",
        "description": "",
        "rules": null,
        "meta": "",
        "productId": 5750501782061056
    },
    {
        "groupId": 5631639635886080,
        "name": "general",
        "description": "",
        "rules": [
            {
                "verb": "GET",
                "path": "/organizations/5714163003293696/*",
                "effect": true
            }
        ],
        "meta": "",
        "productId": 5750501782061056
    },
    {
        "groupId": 5673202705498112,
        "name": "editor",
        "description": "",
        "rules": [
            {
                "verb": "PUT",
                "path": "/organizations/5714163003293696/*",
                "effect": true
            },
            {
                "verb": "POST",
                "path": "/organizations/5714163003293696/*",
                "effect": true
            }
        ],
        "meta": "",
        "productId": 5750501782061056
    }
]

```

Retrieves the details of all groups for a user.

### HTTPS Request

<code style="background:#2196F3;">GET</code> <code style="background:#E3F2FD;">https://[GOODCOP_URL]/v1/user/{userID}/groups</code>

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
userID | required | string | Valid user identifier 

### Returns

Returns list of groups details for a unique userID. If invalid user ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FFFFFF;color:#FF7043;"> 401 </code> `Invalid product API key`  
2.  <code style="background:#FFFFFF;color:#FFC107;"> 400 </code> `User not found`
3.  <code style="background:#FFFFFF;color:#FF0000;"> 500 </code> `We had a problem with our server. Try again later.`
