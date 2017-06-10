--- 

title: Jumpsuit Payments 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

This is Jumpsuit Payments gateway APIs. 

**Version:** 0.1.0 

# Authentication 

|apiKey|*API Key*|
|---|---| 

|apiKey|*API Key*|
|---|---| 

|apiKey|*API Key*|
|---|---| 

|apiKey|*API Key*|
|---|---| 

# /TRANSACTIONS/PAYMENT_PURCHASE
## ***POST*** 

**Summary:** Processing a new payment

**Description:** Processing a payment with new credit card or stored card with option to add a scheduler for recurring payment.

### HTTP Request 
`***POST*** /transactions/payment_purchase` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Success | body | process payment use new credit card | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 401 | failure |
| default | failure |
| 422 (Invalid card) | failure |
| 422 (Invalid Amount) | failure |

# /SCHEDULERS
## ***POST*** 

**Summary:** Create new recurring scheduler

**Description:** Create recurring payment scheduler with credit card information.

### HTTP Request 
`***POST*** /schedulers` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Success 1 | body | create scheduler with new credit card | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| default | failure |
| 500 (Empty input) | failure |
| 422 (Invalid data) | failure |

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
