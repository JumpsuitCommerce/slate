# Errors

The Jumpsuit Payments API uses the following error codes:

> Sample - Error with HTTP code: 500

```json
{
    "errors": [
        "divided by 0"
    ]
}
```

> Sample - Error with HTTP code: 401

```json
{
    "error": "You need to provide correct credentials before continuing."
}
```

> Sample - Error with HTTP code: 403

```json
{
    "errors": [
        "Not authorized to perform requested action."
    ]
}
```

> Sample - Error with HTTP code: 404

```json
{
    "errors": [
        "Couldn't find Scheduler with ... "
    ]
}
```

> Sample - Error with HTTP code: 422

```json
{
    "errors": {
        "amount_cents": [
            "must be greater than 0"
        ]
    }
}
```

```json
{
    "errors": [
        "'afdsaffdas' is not a valid repeat_interval"
    ]
}
```

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is not valid
401 | Unauthorized -- Your API key is not valid
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
422 | Unprocessable Entity - Not allow to process this resource
500 | Internal Server Error -- We had a problem with our server. Try again later.
