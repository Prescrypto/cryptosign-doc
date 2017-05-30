# cryptosign-doc

This is the documentation repository for Cryptosign API. All examples are using [cURL](https://curl.haxx.se/).

## Authentication

Cryptosign uses [OAuth2](https://oauth.net/2/) for securing all the services it provides. You will be given an `access_token` and a `refresh_token` in order to get access to the API.

### Credentials

Contact the admin to get your credentials, you will be given a pair of keys, `client_id` and `client_secret` that corresponds to a valid Cryptosign application.

Open a shell and type:

```shell
curl -X POST -d "grant_type=password&username=<user_name>&password=<password>" -u"<client_id>:<client_secret>" https://cryptosign.herokuapp.com:8000/oauth/token/
```

This services returns:

```javascript
{
  "access_token": "KQ3Yy2vvnY0lKKmwBgFiRfMeOsRNj2",
  "expires_in": 36000,
  "refresh_token": "d3KxGMR727qFSU31KUXQHEhh1IAej2",
  "token_type": "Bearer",
  "scope": "read cryptosign write"
}
```

## Services

### Sign Service

This service provides the capability to sign/hash a PDF file.

Endpoint:
```javascript
https://cryptosign.herokuapp.com/api/v1/sign/
```
Headers:
```javascript
{
  "Authorization": "Bearer KQ3Yy2vvnY0lKKmwBgFiRfMeOsRNj2",
  "Content-Type" : "application/json"
}
```
Request Body:
```javascript
{
	"pdf" : "JVBERi0xLjcKCjEgMCBvYmogICUgZW50cnkgcG9pbnQKPDwKICAvVHlwZSAvQ2F0YWxvZwogIC9QYWdlcyAyIDAgUgo+PgplbmRvYmoKCjIgMCBvYmoKPDwKICAvVHlwZSAvUGFnZXMKICAvTWVkaWFCb3ggWyAwIDAgMjAwIDIwMCBdCiAgL0NvdW50IDEKICAvS2lkcyBbIDMgMCBSIF0KPj4KZW5kb2JqCgozIDAgb2JqCjw8CiAgL1R5cGUgL1BhZ2UKICAvUGFyZW50IDIgMCBSCiAgL1Jlc291cmNlcyA8PAogICAgL0ZvbnQgPDwKICAgICAgL0YxIDQgMCBSIAogICAgPj4KICA+PgogIC9Db250ZW50cyA1IDAgUgo+PgplbmRvYmoKCjQgMCBvYmoKPDwKICAvVHlwZSAvRm9udAogIC9TdWJ0eXBlIC9UeXBlMQogIC9CYXNlRm9udCAvVGltZXMtUm9tYW4KPj4KZW5kb2JqCgo1IDAgb2JqICAlIHBhZ2UgY29udGVudAo8PAogIC9MZW5ndGggNDQKPj4Kc3RyZWFtCkJUCjcwIDUwIFRECi9GMSAxMiBUZgooSGVsbG8sIHdvcmxkISkgVGoKRVQKZW5kc3RyZWFtCmVuZG9iagoKeHJlZgowIDYKMDAwMDAwMDAwMCA2NTUzNSBmIAowMDAwMDAwMDEwIDAwMDAwIG4gCjAwMDAwMDAwNzkgMDAwMDAgbiAKMDAwMDAwMDE3MyAwMDAwMCBuIAowMDAwMDAwMzAxIDAwMDAwIG4gCjAwMDAwMDAzODAgMDAwMDAgbiAKdHJhaWxlcgo8PAogIC9TaXplIDYKICAvUm9vdCAxIDAgUgo+PgpzdGFydHhyZWYKNDkyCiUlRU9G",
	"signatures" : [
	{
		"hash" : "asdldsalkdsaj21j31kl321jk312jk312",
        "email" : "prueba1@trato.io",
		"name" : "Prueba 1"
	},
	{
		"hash" : "sdaklkk213hkj312jkh123hjk123hj2hjk31h",
        "email" : "prueba2@trato.io",
		"name" : "Prueba 2"
	}],
	"params" : {
		"title" : "Titulo",
		"file_name" : "chucho.pdf"
	}
}
```
Open a shell and type:
```shell
curl -X POST \
  https://cryptosign.herokuapp.com/api/v1/sign/ \
  -H 'authorization: Bearer kzjCEcTFwpINAE1pWgzyS6bSafabVW' \
  -H 'content-type: application/json' \
  -H 'postman-token: 47b38b73-8248-e69e-a97d-f89c227a2d6f' \
  -d '{
	"pdf":"JVBERi0xLjcKCjEgMCBvYmogICUgZW50cnkgcG9pbnQKPDwKICAvVHlwZSAvQ2F0YWxvZwogIC9QYWdlcyAyIDAgUgo+PgplbmRvYmoKCjIgMCBvYmoKPDwKICAvVHlwZSAvUGFnZXMKICAvTWVkaWFCb3ggWyAwIDAgMjAwIDIwMCBdCiAgL0NvdW50IDEKICAvS2lkcyBbIDMgMCBSIF0KPj4KZW5kb2JqCgozIDAgb2JqCjw8CiAgL1R5cGUgL1BhZ2UKICAvUGFyZW50IDIgMCBSCiAgL1Jlc291cmNlcyA8PAogICAgL0ZvbnQgPDwKICAgICAgL0YxIDQgMCBSIAogICAgPj4KICA+PgogIC9Db250ZW50cyA1IDAgUgo+PgplbmRvYmoKCjQgMCBvYmoKPDwKICAvVHlwZSAvRm9udAogIC9TdWJ0eXBlIC9UeXBlMQogIC9CYXNlRm9udCAvVGltZXMtUm9tYW4KPj4KZW5kb2JqCgo1IDAgb2JqICAlIHBhZ2UgY29udGVudAo8PAogIC9MZW5ndGggNDQKPj4Kc3RyZWFtCkJUCjcwIDUwIFRECi9GMSAxMiBUZgooSGVsbG8sIHdvcmxkISkgVGoKRVQKZW5kc3RyZWFtCmVuZG9iagoKeHJlZgowIDYKMDAwMDAwMDAwMCA2NTUzNSBmIAowMDAwMDAwMDEwIDAwMDAwIG4gCjAwMDAwMDAwNzkgMDAwMDAgbiAKMDAwMDAwMDE3MyAwMDAwMCBuIAowMDAwMDAwMzAxIDAwMDAwIG4gCjAwMDAwMDAzODAgMDAwMDAgbiAKdHJhaWxlcgo8PAogIC9TaXplIDYKICAvUm9vdCAxIDAgUgo+PgpzdGFydHhyZWYKNDkyCiUlRU9G",
	"signatures" : [
	{
		"hash" : "asdldsalkdsaj21j31kl321jk312jk312",
		"email" : "prueba1@trato.io",
		"name" : "Prueba 1"
	},
	{
		"hash" : "sdaklkk213hkj312jkh123hjk123hj2hjk31h",
		"email" : "prueba2@trato.io",
		"name" : "Prueba 2"
	}],
	"params" : {
		"title" : "Titulo",
		"file_name" : "prueba.pdf"
	}
}'
```

You should receive your PDF file and a sheet appended at the end, like the following:

![screenshot](assets/screenshot.png)

### Postman Collection

If you use [Postman](https://www.getpostman.com/) for testing the API, in the `assets` directory you will find the `cryptosign_test.postman_collection` file. Just import it to your existing collections.

![postman](assets/postman.png)
