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

```json
{
    "errors": [
        "'afdsaffdas' is not a valid repeat_interval"
    ]
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

> Sample - Error with HTTP code: 401

```json
{
    "error": "You need to provide correct credentials before continuing."
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
    "errors": {
        "amount_cents": [
            "must be greater than 0"
        ],
        "credit_card.number": [
            "can't be blank",
            "is required"
        ]
    }
}
```


Error Code | Meaning
---------- | -------
500 | Internal Server Error -- We had a problem with our server. Try again later.
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
401 | Unauthorized -- Your API key is not valid
422 | Unprocessable Entity - Not allow to process this resource

<aside class="notice">
Error response in JSON format varies according to the HTTP reponse code
</aside>

Error Code | Root Key | Content
---------- | -------  | -------
500, 403, 404 | errors | array of strings
401 | error | string
422 | errors | hash with key(attribute name) -> content(array of strings)
