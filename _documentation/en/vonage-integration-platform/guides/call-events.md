---
title: Call Events
---
# Call Events

Events representing the state of telephone calls all share common fields and meanings, whether they are delivered in response to call control methods, or by querying for events, or delivered via webhook. All call events have the following properties:

| Property | Description |
| -------- | ------------|
| id          | The unique id of the event |
| userId      | The VIS user id associated with the event |
| accountId   | The VIS account id associated with the event |
| externalId  | The unique id of the event provided by the external communications provider, only used for informational purposes |
| direction   | Either INBOUND or OUTBOUND |
| phoneNumber | The phone number of the remote party |
| callerId    | The name of the remote party |
| state       | The call state, see Event States below |
| duration    | The length of the call (in milliseconds) |
| startTime   | An ISO-8601 date/time when the call started. For outbound, the start time marks when the call is placed; for incoming calls, it marks the time the call was first received |
| answerTime  | An ISO-8601 date/time when the call was answered |
| endTime     | An ISO-8601 date/time when the call ended |

## Event States

The VIS APIs present a simple event state model for telephone calls, hiding the differences and complexities of either Vonage Business Cloud™ and Vonage Enterprise. These event states are delivered in response to method APIs (e.g. place call, get calls) and included in webhook event notifications. Understanding the event state model is critical to building external integrations.

The following finite state machine describes the allowable state transitions:

The only initial state is Initializing. The only allowable ending states are Answered, Cancelled, Rejected, and Missed. Call states in one of the final ending states will always remain in the ending state.

| State | Initial? | Final? | Direction | Allowable Transitions | Description |
| ----- | -------- | ------ | --------- | --------------------- | ----------- |
| Initializing | Y | N | Inbound           | Ringing, Answered                              | A call has been placed but the remote party has not yet been alerted | 
| Ringing      | N | N | Inbound, Outbound | Active, Answered, Cancelled, Rejected, Missing | The remote party is being alerted (outbound) or an inbound call is occurring |
| Active       | N | N | Inbound, Outbound | Answered, Held, Remote Held                    | A call is active and the participants are speaking |
| Held         | N | N | Inbound, Outbound | Active                                         | An active call is currently on hold |
| Remote Held  | N | N | Inbound, Outbound | Active                                         | A remote party of an active call is currently on hold |
| Answered     | N | Y | Inbound, Outbound |                                                | A call of non-zero duration has ended | 
| Cancelled    | N | Y | Outbound          |                                                | An outbound call has been cancelled before the remote party answered | 
| Missed       | N | Y | Inbound           |                                                | An incoming call was not answered |
| Rejected     | N | Y | Inbound           |                                                | An incoming call was rejected or sent to voicemail without being answered |

For every state, the values for startTime, answerTime, endTime, and duration will follow certain rules. All call states will have a valid startTime. Only Active, Held, Remote Held, and Answered will have a valid answerTime. The endTime property will remain null until the call reaches a final state (Answered, Cancelled, Missed, Rejected). Only calls that have reach the final Answered state will have a non-zero duration.

## Getting Call Events

The API supports retrieving call events for either active or ended calls. Because the number of call event records may be numerous, the response may be paged. Typically, applications retrieve the total number of records for a particular set of query parameters and then retrieve the events over a span of multiple API calls using the same set of query parameters and a maximum number of events to return per call.