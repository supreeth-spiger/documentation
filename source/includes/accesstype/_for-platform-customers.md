# For Platform Customers

The customers of Quintype platform can use below APIs for subscriptions in Accesstype.

## POST Register And Subscribe a user

```shell
curl -H "X-QT-AUTH: sample-auth" -H "Content-Type: application/json" http://sketches.quintype.com/api/v1/register-and-subscribe -d '{
   "member": {
        "email": "ace33@quintype.com",
        "username": "ace 33",
        "password": "password",
        "name": "ace 33",
        "dont-login": false
    },
    "options": {
        "gateway-name": "razorpay"
    },
    "payment": {
        "attributes": {
            "currency": "INR",
            "amount": 100,
            "payment-type": "Razorpay",
            "gateway-payment-id": "pay_123trt465",
            "attributes": ""
        }
    },
    "subscription": {
        "accesstype-plan-id": 4,
        "currency": "INR",
        "amount": 100,
        "metadata": {
          "city": "Bangalore",
          "state": "Karnataka",
          "house": "Old Airport Road, Murugeshpallya, Bangalore",
          "street": "Old Airport Road, Murugeshpallya, Bangalore",
          "landmark": "Karnataka",
          "pincode": "560017",
          "mobile": "8129612361"
         }

    }}
'

```
Registers a member and creates subscription in Accesstype. It returns X-QT-AUTH in response headers.

`gateway-name` can be any valid payment-type suppored by Accesstype.

`accesstype-plan-id` is the Id of plan in Accesstype.


## POST Subscribe Without Login

```shell
curl -H "Content-Type: application/json" http://sketches.quintype.com/api/v1/subscribe-without-login?email=example@gmail.com -d '{
    "options": {
        "gateway-name": "razorpay"
    },
    "payment": {
        "attributes": {
            "currency": "INR",
            "amount": 100,
            "payment-type": "Razorpay",
            "gateway-payment-id": "pay_123trt465",
            "attributes": ""
        }
    },
    "subscription": {
        "accesstype-plan-id": 4,
        "currency": "INR",
        "amount": 100,
        "metadata": {
          "city": "Bangalore",
          "state": "Karnataka",
          "house": "Old Airport Road, Murugeshpallya, Bangalore",
          "street": "Old Airport Road, Murugeshpallya, Bangalore",
          "landmark": "Karnataka",
          "pincode": "560017",
          "mobile": "8129612361"
         }

    }}
'

```
It create subscription for a already registered user.
`gateway-name` can be any valid payment-type suppored by Accesstype.

`accesstype-plan-id` is the Id of plan in Accesstype


## LIST All subscriptions of a user

```shell
curl -H "X-QT-AUTH: <your-auth-token>" http://sketches.quintype.com/api/v1/members/me/subscriptions

{
 "subscriptions":[
  {
     "id":713,
     "subscriber_id":453,
     "subscription_plan_id":16,
     "created_at":"2017-10-30T10:55:42.201Z",
     "updated_at":"2017-10-30T10:55:42.201Z",
     "assets":[

     ],
     "start_timestamp":"2017-10-30T10:55:42.176Z",
     "end_timestamp":"2017-11-13T10:55:42.176Z",
     "deleted_at":null,
     "payment_id":668,
     "metadata":{
        "Name":"Sample User",
        "Address":"Sample add",
        "Phone Number":"1111111111"
     },
     "external_id":null,
     "trial_period_length":null,
     "trial_period_unit":null,
     "coupon_code":null,
     "subscription_group_id":21,
     "preferred_identity":{
        "provider":"email",
        "value":"sample@gmail.com"
     },
     "group_name":"Sub Group 1",
     "plan_name":"Sub Plan 1",
     "duration_length":2,
     "duration_unit":"weeks",
     "subscription_type":"individual",
     "active":true,
     "payment_amount":"0.00",
     "payment_type":"manual"
    }
  ]
}
```
It gives all subscriptions for a user.

This API is safe to call from the front end JS, where it will read session-cookie to determine the current user. Backend callers can use X-QT-AUTH for the same purpose.

## LIST All Assets accessible to a user

```shell
curl -H "X-QT-AUTH: <your-auth-token>" http://sketches.quintype.com/api/v1/members/me/assets

{
   "assets":[
      {
         "type":"site"
      },
      {
         "type":"site"
      },
   ]
}
```
It gives all assets accessible to a user.

This API is safe to call from the front end JS, where it will read session-cookie to determine the current user. Backend callers can use X-QT-AUTH for the same purpose.

## PATCH Update a subscription

```shell
curl -H "X-QT-AUTH: <your-auth-token>" -X "PATCH" http://sketches.quintype.com/api/v1/members/me/subscriptions/<id> -d '{
  "metadata":  {
    "full-name": "hello-world",
    "email": "hello@quintype.com"
  }
}`

```
It updates a subscription for user.

This API is safe to call from the front end JS, where it will read session-cookie to determine the current user. Backend callers can use X-QT-AUTH for the same purpose.

## PATCH Update all subscriptions

```shell
curl -H "X-QT-AUTH: <your-auth-token>" -X "PATCH" http://sketches.quintype.com/api/v1/members/me/subscriptions -d '{
  "metadata":  {
      "full-name": "hello-world",
      "email": "hello@quintype.com"
  }
}`

```
It bulk updates all subscriptions for user.

This API is safe to call from the front end JS, where it will read session-cookie to determine the current user. Backend callers can use X-QT-AUTH for the same purpose.