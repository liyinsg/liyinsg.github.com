---
layout: post
title: "Google Cloud Messaging"
---
![System Architecture](https://developers.google.com/cloud-messaging/images/notifications-overview.svg)

### Notifications vs data messages

  |Feature|Notifications|Data Messages|
  |---|---|---|
  |Size|<=2KB|<=4KB|
  |Collapsible|Forced|default no|
  |Notification tray|True|False|

### Messaging options
* High priorty message will wake a sleeping device when possible
* set time_to_live = 0 means messages that can’t be delivered immediately will be discarded

### Topics
* 2KB limit
* Path must mathces regex `/topics/[a-zA-Z0-9-_.~%]+`
* "to" field will set to topic path instead of [registration token](https://developers.google.com/instance-id/)
* registration token is not needed

### Device Groups
* Typically, "group" refers a set of different devices that belong to a single user
* 2KB for iOS, 4KB for other platforms
* registration token is needed
* Group registration tokens by notification_key
* Maximum number of member for each notication_key is 20

### GCM Client
* [GCM Network Manager](https://developers.google.com/cloud-messaging/network-manager)
* [GCM Network Manager Quickstart](https://github.com/googlesamples/android-gcmnetworkmanager)
* [GoogleCloudMessaging](https://developers.google.com/android/reference/com/google/android/gms/gcm/GoogleCloudMessaging)

### GCM XMPP server
  * [XMPP connection server reference](https://developers.google.com/cloud-messaging/xmpp-server-ref#downstream-xmpp-messages-json)
  * [XMPP app server sample](https://github.com/googlesamples/gcm-playground)
  * production: gcm-xmpp.googleapis.com:5235
  * testing: gcm-preprod.googleapis.com:5236
  * 1000 connections in parallel for each [sender ID](https://developers.google.com/cloud-messaging/gcm#senderid)
  * CCS may send `CONNECTION_DRAINING` message to indicate that the connection is being drained and will be closed soon
  * `delivery_receipt_requested` is for Downstream only?
  * Flow control
    * Every message sent to CCS receives either an ACK or a NACK response.
    * Messages that haven't received one of these responses are considered pending.
    * If the pending message count reaches 100, the [app server](https://developers.google.com/instance-id/reference/server) should stop sending new messages and wait for CCS to acknowledge 

### HTTP vs XMPP

  |Feature|HTTP|XMPP|
  |---|---|---|
  |Direction|Downstream only|Both|
  |Call|Synchronous|Asynchronous|
  |Json|HTTP Post|encapsulated in XMPP|
  |Multicast downstream|Supported|Not supported|

