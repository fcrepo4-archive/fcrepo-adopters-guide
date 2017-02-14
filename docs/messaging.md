# Messaging

## Introduction

As with Fedora 3 and Fedora 4, repository events will generate messages that are published on a message broker
(for example: ActiveMQ). These messages can be consumed by external applications written in any language.

In Fedora 3, these messages were serialized in Atom XML along with some Fedora-specific header values. Messages were emitted whenever there was a change to a repository resource (i.e. an API-M operation).

In Fedora 4, these messages are serialized in JSON-LD with some Fedora-specific header values. Similarly, messages
are emitted whenever a repository resource is changed (i.e. an Update/Create/Delete operation).

According to the Fedora API specification, messages will still be emitted whenever a resource changes (i.e. an
Update/Create/Delete operation); the significant difference will be with the serialization format.

## Message Serialization

Previous Fedora systems used a standardized framing mechanism to structure messages: both Atom and JSON-LD specify
the structure of a message, while allowing message writers considerable flexibility with the content of the documents.
Having an open-ended message format, however, makes it considerably more difficult to write a message consumer that
isn't just tied to the specific flavor of Atom or JSON-LD that is chosen.

The Fedora API specification continues to use a clearly specified framing format (JSON-LD), but it goes further to
make use of a clearly specified content format (ActivityStreams 2.0). By requiring that all messages conform to the
AS 2.0 specification, it means that _any_ AS 2.0 reader can consume repository messages.

Activity Streams 2.0 mandates a minimal set of required data properties for messages along with a set of optional properties.
Because the format is JSON-LD, it is still possible for any valid JSON-LD to be part of a message, while still conforming
to the AS 2.0 specification.

## Serialization Examples

A very simple message could look like:

```
{
  "@context" : [
    "https://www.w3.org/ns/activitystreams" , {
    "date" : {
        "@id" : "http://purl.org/dc/terms/date",
        "@type": "xsd:dateTime" } } ] ,
  "type" : "Create" ,
  "id" : "urn:uuid:3c834a8f-5638-4412-aa4b-35ea80416a18" ,
  "date" : "2016-05-19T17:17:39Z" ,
  "actor" : "http://example.org/user/fedoRaadmin" ,
  "object" : {
    "id" : "http://example.org/repository/resource" ,
    "type" : [ "ldp:Container" , "ldp:RDFSource" ] } ,
  "inbox" : "http://example.org/receiver/inbox"
}
```

Here, the `type` of the event is `Create`, which expands to `as:Create` or `http://www.w3.org/ns/activitystreams#Create`.
Other types that can be expected of a Fedora implementation include: `Delete` and `Update`.

The `id` field corresponds to a unique identifier for the event itself. Implementations may use different mechanisms to
ensure uniqueness and to format identifiers.

The `date` field will be an ISO 8601 DateTime field.

The `actor` field will correspond to the agent that triggered this event. The value of this field can be either a URI
(as in this example) or a structured value such as:

```
"actor" : {
    "id" : "#agent" ,
    "type" : "Person" ,
    "name" : "fedo raAdmin" }
```

Furthermore, the `actor` field may contain multiple values:

```
"actor" : [ "http://example.org/user/fedoRaadmin", {
    "id" : "#agent" ,
    "type" : "Application" ,
    "name" : "FcrepoClient/0.1" } ]
```

The `object` field will reference the Fedora resource that corresponds to the event. It can be referred to as
a simple URI: `"object" : "http://example.org/repository/resource"`, though the Fedora specification recommends (`SHOULD`)
that the RDF Types of a resource be included in a message. Thus, the longer form may be more common:

```
"object" : {
    "id" : "http://example.org/repository/resource" ,
    "type" : [ "ldp:Container" , "ldp:RDFSource" ] }
```

Finally, the `inbox` field expands to `ldp:inbox` or `http://www.w3.org/ns/ldp#inbox`. This field is optional; not all
resources will even have a `ldp:inbox` reference. For more information about the meaning of this field, please consult
the [Linked Data Notifications](https://www.w3.org/TR/ldn/) specification.

## Changes from Fedora4

Early versions of Fedora4 (before version 4.6.0) emitted header-only messages. Headers are not part of the Fedora API
specification; nor are they part of the Activity Streams specification. Any client software that relies on message
header values will need to be modified.

Starting with Fedora 4.6.0, JMS messages contained both headers and a JSON-LD body. That body does not conform with
the Activity Streams specification.

In the change to using Activity Streams, the structure of the JSON-LD document will change somewhat from what it is in
Fedora 4.6.0 and later. The most significant changes, however, will be that the event types will make use of the
[Activity Streams vocabulary](https://www.w3.org/TR/activitystreams-vocabulary/) instead of a Fedora-specific event
vocabulary. Any messaging application making use of a Fedora-specific event type will need to be modified to use the
Activity Streams vocabulary types.

## Message Broker Technology

Both Fedora 3 and Fedora 4 have made use of an embedded ActiveMQ broker, which typically produced JMS messages on
the OpenWire and Stomp protocols. The messaging portion of the Fedora specification is silent on broker technology.
An implementation is free to use whatever broker technology is deemed appropriate: AMQP (e.g. RabbitMQ), JMS (e.g. ActiveMQ),
XMPP, WebSockets, Kafka, etc. Messaging clients should take this into consideration.

