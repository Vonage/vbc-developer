---
title: Webhooks
---
# Webhooks

Webhooks allow developers to register URLs that receive notification of events for users via HTTP. Every registered webhook is uniquely identified by a globally unique id; all subsequent operations take this id in the resource path.

## External Endpoints

Webhooks must support POST and respond with an Http Status 200 within the required timeout, otherwise the delivery will be retried. Webhook notifications are retried a maximum of 5 times, pausing 10 seconds between retries, before the webhook is marked as failed. Subsequent events are not delivered to failed webhooks. Renewing a webhook will clear its "failed" status and will start receiving event notifications once again.

Webhook endpoints must respond in a timely fashion. Our system must be able to establish a connection to the webhook URL server within 3 seconds and the Http Status 200 must be received within 2 seconds in order for the webhook delivery to be marked as a success.

## Expiration

Webhook registrations expire after some period of time (expireAt, typically 10 days) after which they will no longer receive notifications. Expired (or non-expired) webhooks may be renewed indefinitely, however. Expired webhooks will be permanent expunged at some point (purgeAt). When a webhook is renewed, the renewedAt and renewedBy properties are set to the current time, and the expireAt and purgeAt properties are reset to new values after renewedAt.

When a webhook is renewed it resets the failure flag, but it does not remove any other past delivery statistics.

## Metadata, Signatures, & Deduplication

Along with every webhook notification event, metadata about the webhook event and its delivery can either be included in the HTTP header, the request body itself, or not at all. The metadataPolicy property controls the desired metadata delivery.

Webhook metadata consists of the following properties:

| Key | Description |
| --- | ----------- |
| signature  | The hashed value of the webhook event. If policy is HEADER, this value is sent as X-VON-Signature |
| webhookId  | The unique id of the webhook. If the policy is HEADER, this value is sent as X-VON-Webhook-Id |
| deliveryId | A unique id identifying the specific event delivery. If the policy is HEADER, this value is sent as X-VON-Delivery-Id |
| attempt    | Identifies the number of times the event has been attempted to be delivered for the same deliveryId. If the policy is HEADER, this value is sent as X-VON-Attempt |

In order for this metadata to be delivered, metadataPolicy must be set to either HEADER or BODY. Additionally, the signature is only set if signingAlgo is set to HMAC_SHA256 and a non-empty signingKey is set.

Since the system retries delivery for webhook entries that have timed-out, the endpoint itself needs to know whether multiple POSTs to a URL represent the same or different event. The deliveryId and attempt properties provide the endpoint the necessary information to distinguish between separate notification events versus retries.

## Events

Webhook notification events have the following format, for example:

```json
{
  "event" : {
    "id" : "5a85d86f253bcd10897f3189",
    "externalId" : "callhalf-60227142553:0",
    "userId" : "24785",
    "accountId" : "376",
    "type" : "CALL",
    "direction" : "OUTBOUND",
    "duration" : 2950,
    "state" : "ANSWERED",
    "startTime" : "2018-02-15T18:58:56.194+0000",
    "answerTime" : "2018-02-15T18:59:03.496+0000",
    "endTime" : "2018-02-15T18:59:06.446+0000"
  },
  "metdata" : {
    "signature" : "95aafd08cb72b1f9216ccd002b8917b04e41ecb19276ae759241fdc0cbb53fb5",
    "webhookId" : "7dc53df5-703e-49b3-8670-b1c468f47f1f",
    "deliveryId" : "0debd31c-68e7-4d5a-be7e-52e8870ca4d6",
    "attempt" : 1
  }
}
```

The metadata property is only included if metadataPolicy is set to BODY. The signature, a hex-encoded string, is computed from the json value of the event property, where all properties are sorted alphabetically with no whitespace between property names or their values. For example, the signature on the above example event body would be computed on the following json:

```json
{"accountId":"376","answerTime":"2018-02-15T18:59:03.496+0000","direction":"OUTBOUND","duration":2950,"endTime":"2018-02-15T18:59:06.446+0000","externalId":"callhalf-60227142553:0","id":"5a85d86f253bcd10897f3189","startTime":"2018-02-15T18:58:56.194+0000","state":"ANSWERED","type":"CALL","userId":"24785"}
```

And using the secret key mysecretkey would have the following signature: 

```95aafd08cb72b1f9216ccd002b8917b04e41ecb19276ae759241fdc0cbb53fb5.```

## Redirection Policy

Webhook endpoints are permitted to return either Http Status 302 or 307. The system will follow redirects, up to some limit, after which, the system will mark the webhook as failed. If the webhook endpoint returns a 302, then the webhook event is delivered as an Http Get to the URL found in the response Location header. If a 307 is returned, then the webhook event is delivered as an Http POST to the URL found in the response Location header.

## Statistics

The system keeps track of the total number of attempts, successes and failures. It also keeps track of the date/time of the last success and failure. For failures, the most recent Http status code and descriptive message are also kept. When a webhook is renewed only the isFailed property is reset back to false; all other statistics are kept for informational purposes.

A webhook is not considered either a success or failure until all of the retry attempts for a particular delivery have been exhausted. For example, if system retries a webhook delivery five times and fails, it counts as a single additional attempt and failure.

Webhook statistics can be used to discover events that are potentially missed if the URL is temporarily unavailable (for example, because of system maintenance). In such a case, missed events can be queried for that happened after lastSuccess. It is good practice to renew any existing webhooks immediately after a system is restored following maintenance.