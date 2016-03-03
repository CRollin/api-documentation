## Quick start

MakeupOnUs has a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) that allows to third party developers to integrate our face recognition and automatic makeup features on their own projects.

### Base Url
The main endpoint can be accessed throught `https://www.makeupon.us/api/v1`, please note the `https`, whiles it is not currently enforced, it is strongly recommended to use it in order to avoid security risks.

## Authentication

verb | resource
-----|-------------
POST | /auth

params | descrption
-------|-----------
none | -

In order to use our API, you must request an authentication token to sign the resquests, this can be done by requesting a **POST** call to the `/auth` route using [HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication), where the user and password are the **api_key** and **api_secret** given to you at the registration process.

Using curl, the authentication process is the following:
```
curl -u api_key:api_secret https://www.makeupon.us/api/v1/auth
```
This post, should return a json with one of the following scenarios:

**Success response:**
```javascript
{
	'status': 'success',
	'message': 'ok',
	'auth_token': 'j878g39yx378pa77djthzzpn34.aHtyLds234'
}
```

**Failure response:**
```javascript
{
	'status': 'fail',
	'message': 'Wrong credentials',
	'auth_token': null
}
```

You should store **auth_token** to sign the future requests.

## Sing requests

To sign a request simple add an `Authentication: Bearer auth_token` header to our calls, using **curl** and our example avobe the call should be signed as:

```
curl -H "Authentication: Bearer j878g39yx378pa77djthzzpn34.aHtyLds234" https://www.makeupon.us/api/v1/mycall
```

If your token is valid you should get an **HTTP 201** response and you call will be processed by the server, otherwise you'll get a **HTTP 403**.

## Using the API

### Getting products

verb | resource
-----|-------------
POST | /*user*/products

where *user* is you api_key.

params | descrption
-------|-----------
none | -

In order to get the products from our database you should call `<user>/products` endpoint, that will return a json containing the information about the products related to your account.

```javascript
{
	'status': 'success',
	'message': 'ok',
	'products': {
		{
			'id': 'WexYt3z',
			'color': '#982328',
			'ref': 'lipstick-glam-01',
			'type': 12
		}
	}
}
```

Where the product object is represented as:

name   | descrption
-------|-----------
Id     | MakeupOnUs Id for the product, this is used to process the images whithin a product
Color  | The key color of the product, useful if you want to personalize elements on your interface
Ref    | An external unique reference to your own database, it can be the product id on your table, the product name, SKU, etc.
type   | the type of product

### Uploading user pictures


### Process a picture




