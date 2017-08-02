---

title: Jumpsuit Payments API

language_tabs:
  - shell

toc_footers:
#   - <a href='#'>Sign Up for a Developer Key</a>
#   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a>

includes:
   - errors

search: true

---

# Introduction

These are Jumpsuit Payments gateway APIs.

**Protocol:** https

**Format:** JSON

**Version:** 0.1.0


# Authentication

There are two ways to authenticate API calls

### Use query parameters

Example:

`https://jumpsuitpayments.com/api/transactions/payment_purchase?api_username=[your_user_name]&api_key=[your_api_key]`

|Name|Type|Description|
|---|---|---|
|api_username|String|The unique account shared by both API call and Web access|
|api_key|String|The API specific authentication token assigned to your account. Can be found at web portal|

### Use http headers

Example:

`https://jumpsuitpayments.com/api/transactions/payment_purchase`

`X-Api-Username: [your_user_name]`

`X-Api-Key: [your_api_key]`

|Name|Type|Description|
|---|---|---|
|X-Api-Username|String|The unique account shared by both API call and Web access|
|X-Api-Key|String|The API specific authentication token assigned to your account. Can be found at web portal|

# Payments

## Purchase

> Process a payment with a new credit card

```shell
curl -X POST \
  http://www.minigator.devel:5001/api/transactions/payment_purchase \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: ca25c6dd-8080-420f-0ef7-96f680d4ac38' \
  -H 'x-api-key: MinigatorAuthenticationToken' \
  -H 'x-api-username: minigator' \
  -d '{
	"transaction":
	{
	  "amount_cents": "100",
	  "credit_card_attributes":
	  {
		"number": "4470330769941000",
		"first_name": "Bin",
		"last_name": "Li",
		"expiration_date": "12/2017",
		"verification_value": "123"
	  }
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "transaction": {
        "id": "dd26043f-327e-4388-a05e-d5e0c666764c",
        "transaction_type": "payment_purchase",
        "source": null,
        "processed_at": "2017-06-24T01:35:37.206Z",
        "status": "success",
        "email": null,
        "description": null,
        "amount_cents": 100
    }
}
```

> Process a payment with a new credit card and store it

```shell
curl -X POST \
  http://www.minigator.devel:5001/api/transactions/payment_purchase \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: ca25c6dd-8080-420f-0ef7-96f680d4ac38' \
  -H 'x-api-key: MinigatorAuthenticationToken' \
  -H 'x-api-username: minigator' \
  -d '{
	"transaction":
	{
	  "amount_cents": "100",
	  "credit_card_attributes":
	  {
		"number": "4470330769941000",
		"first_name": "Bin",
		"last_name": "Li",
		"expiration_date": "12/2017",
		"verification_value": "123",
    "store_me": "true"
	  }
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "transaction": {
        "id": "c8fce3ff-816a-4691-8720-3ca59edada32",
        "transaction_type": "payment_purchase",
        "source": null,
        "processed_at": "2017-06-24T01:45:55.250Z",
        "status": "success",
        "email": null,
        "description": null,
        "amount_cents": 100,
        "credit_card": {
            "id": "8eefff1c-2de9-446b-90ab-63161efcb0a7",
            "name": "8eefff1c-2de9-446b-90ab-63161efcb0a7",
            "card_brand": "visa",
            "last_four": "1000",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
e
```

> Process a payment with a new credit card and schedule recurring payments at same time

```shell
# The credit card will be stored automatically for recurring payments purpose
curl -X POST \
  'http://www.minigator.devel:5001/api/transactions/payment_purchase?api_username=minigator&api_key=MinigatorAuthenticationToken' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 6747dff6-b8d8-62b8-65cf-3935bf4a3915' \
  -d '{
	"transaction":
	{
	  "amount_cents": "300",
	  "credit_card_attributes":
	  {
		"number": "4470330769941000",
		"first_name": "Bin",
		"last_name": "Li",
		"expiration_date": "2017/12/1",
		"verification_value": "123"
	  },
	  "scheduler_attributes":
	  {
		"starts_at": "2017/12/1",
		"repeat_interval": "daily"	  	
		"max_repeat_count": "11"	  	
	  }
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "transaction": {
        "id": "d504a9d0-696f-467f-b8b9-c16f2db9e42f",
        "transaction_type": "payment_purchase",
        "source": null,
        "processed_at": "2017-06-24T01:59:17.223Z",
        "status": "success",
        "email": null,
        "description": null,
        "amount_cents": 300,
        "scheduler": {
            "id": "2d38706f-59cd-42ac-bf4d-f93e72ec5e8d",
            "starts_at": "2017-12-01",
            "repeat_interval": "daily",
            "status": "active",
            "amount_cents": 300
        },
        "credit_card": {
            "id": "0f486731-3c2a-47c8-877e-3b83e2f9ccb4",
            "name": "0f486731-3c2a-47c8-877e-3b83e2f9ccb4",
            "card_brand": "visa",
            "last_four": "1000",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
}
```

> Process a payment with a stored credit card

```shell
curl -X POST \
  'http://www.minigator.devel:5001/api/transactions/payment_purchase?api_username=minigator&api_key=MinigatorAuthenticationToken' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 6747dff6-b8d8-62b8-65cf-3935bf4a3915' \
  -d '{
	"transaction":
	{
	  "amount_cents": "100",
	  "credit_card_id": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5"
	}
}'
```


>> The above code returns JSON structured like this:

```json
{
    "transaction": {
        "id": "3272475d-24ad-450f-a577-5e0e830d1d7d",
        "transaction_type": "payment_purchase",
        "source": null,
        "processed_at": "2017-06-24T02:02:29.887Z",
        "status": "success",
        "email": null,
        "description": null,
        "amount_cents": 200,
        "credit_card": {
            "id": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5",
            "name": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5",
            "card_brand": "visa",
            "last_four": "1111",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
}
```

> Process a payment with a stored credit card and schedule a recurring payments

```shell
curl -X POST \
  'http://www.minigator.devel:5001/api/transactions/payment_purchase?api_username=minigator&api_key=MinigatorAuthenticationToken' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 6747dff6-b8d8-62b8-65cf-3935bf4a3915' \
  -d '{
	"transaction":
	{
	  "amount_cents": "200",
	  "credit_card_id": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5",
	  "scheduler_attributes":
	  {
		"starts_at": "2017/12/1",
		"repeat_interval": "daily"	  	
	  }
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "transaction": {
        "id": "4c2ee9b8-69e6-40f4-b783-0e337e31bb30",
        "transaction_type": "payment_purchase",
        "source": null,
        "processed_at": "2017-06-24T02:05:19.258Z",
        "status": "success",
        "email": null,
        "description": null,
        "amount_cents": 200,
        "scheduler": {
            "id": "a1bd8ffd-453b-4912-b5c4-ccd1566dfbc1",
            "starts_at": "2017-12-01",
            "repeat_interval": "daily",
            "status": "active",
            "amount_cents": 200
        },
        "credit_card": {
            "id": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5",
            "name": "6ba38f63-f10f-40e6-bc50-f672e75e1fd5",
            "card_brand": "visa",
            "last_four": "1111",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
}
```

**Summary:** Processing a new payment

**Description:** Processing a payment with new credit card or stored card with option to add a scheduler for recurring payment.

### HTTP Request
`POST /transactions/payment_purchase`



# Schedulers

## Create

> Create a recurring schedule using a new credit card

```shell
curl -X POST \
  'http://www.minigator.devel:5001/api/schedulers?api_username=minigator&api_key=MinigatorAuthenticationToken' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: a5617447-c218-5105-70d9-20163b21faef' \
  -d '{
	"scheduler":
	{
		"amount_cents": "800",
		"starts_at": "2017/12/1",
		"repeat_interval": "daily",
		"credit_card_attributes":
		{
			"number": "4470330769941000",
			"first_name": "Bin",
			"last_name": "Li",
			"expiration_date": "2017/12/1",
			"verification_value": "123"
		}
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "scheduler": {
        "id": "6892fb8a-d583-40d9-aacd-263a28eb5506",
        "starts_at": "2017-12-01",
        "repeat_interval": "daily",
        "status": "active",
        "amount_cents": 800,
        "credit_card": {
            "id": "d0c307f4-6d1b-4d12-8fec-b6c4feef2dd0",
            "name": "d0c307f4-6d1b-4d12-8fec-b6c4feef2dd0",
            "card_brand": "visa",
            "last_four": "1000",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
}
```

> Create a recurring schedule using a stored credit card

```shell
curl -X POST \
  'http://www.minigator.devel:5001/api/schedulers?api_username=minigator&api_key=MinigatorAuthenticationToken' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: cd426235-3e80-2ff2-e454-46a6c9544167' \
  -d '{
	"scheduler":
	{
		"amount_cents": "11",
		"starts_at": "2017-07-26",
		"repeat_interval": "daily",
		"credit_card_id": "15d30739-e191-430f-af75-532aea0a1739"
	}
}'
```

>> The above code returns JSON structured like this:

```json
{
    "scheduler": {
        "id": "d617978a-95e2-4965-bdcf-363b9c8c704c",
        "starts_at": "2017-07-26",
        "repeat_interval": "daily",
        "status": "active",
        "amount_cents": 11,
        "credit_card": {
            "id": "15d30739-e191-430f-af75-532aea0a1739",
            "name": "15d30739-e191-430f-af75-532aea0a1739",
            "card_brand": "visa",
            "last_four": "1000",
            "expiration_date": "2017-12-01",
            "store_me": true,
            "first_name": "Bin",
            "last_name": "Li",
            "address1": null,
            "address2": null,
            "city": null,
            "state": null,
            "zip": null,
            "country": null,
            "phone": null
        }
    }
}
```
**Summary:** Create new recurring scheduler

**Description:** Create recurring payment scheduler with credit card information.

### HTTP Request
`POST /schedulers`
