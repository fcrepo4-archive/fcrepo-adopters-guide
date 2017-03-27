# Versioning

## Introduction

The Fedora API specification conforms to the [Memento](https://mementoweb.org/guide/rfc/)
specification and brings with it all the versioning capabilities of the Memento
framework along with some new features.  Below we will review some of the core Memento
concepts as well as compare the Fedora API's new approach to versioning (i.e. Memento) with
Fedora 4 way of doing things.


## Overview of the New Memento Hotness

The Memento specification defines three important concepts, `Mementos`, `TimeGates`,
and `TimeMaps`.  You may find [this diagram](http://mementoweb.org/guide/quick-intro/)
helpful in gaining an overall understanding of how API works.  

A `Memento` is a  prior version of an `Original Resource` which is to say an encapsulation of the
resource's state on at a particular moment in time.  In the case of immutable or
static resources such as tweets, it is possible that the `Original Resource`
and the `Memento` are identical.

A `TimeGate` is simply a resource that, when given  a date time, will resolve a
memento that most closely represents the state of the `Original Resource` on that date.  
Instead of having to know the exact date of the memento  you wish to retrieve, the
`TimeGate` essentially allows you to query the set of mementos for the closest match.  
Depending on the interaction model, the `TimeGate`  may return the available time range,  
the closest memento, the first and last mementos in the set, and the next and previous mementos relative
to the closest match.

A related resource is the `TimeMap`.  The `TimeMap` resource returns the set of
mementos within a specified time range as well as first and last mementos for the
original resource.  In other words,  the `TimeMap`  lets you query the resource for
previous versions using a date range.

With this basic overview of Memento,  let's look at how the Fedora API specification,
with its Memento support, compares to the older Fedora 4 interaction model.

For details about the `Memento`, take a look at the [specification](https://tools.ietf.org/html/rfc7089).

## Old vs New

### Version Creation

While Fedora 4  supports client controlled version creation, the Fedora API Spec defines this behavior as optional.  Instead, it is up to the implementation to decide whether versioning is client and/or server managed.


### List all versions of a resource

*Fedora 4*

```
curl  http://localhost:8080/rest/your-resource/fcr:versions
```

*Fedora API Spec*

```
@TODO to be filled in
```

### Get previous version a resource

*Fedora 4*

```
curl http://localhost:8080/rest/resource/fcr:versions/<version-label>

```

*Fedora API Spec*

```
@TODO to be filled in
```

### Revert to a previous version of an object

*Fedora 4*

```
curl -X PATCH http://localhost:8080/rest/path/to/resource/fcr:versions/<existing-version-name>

```

*Fedora API Spec*

```
Optional: It is up to the implementation to decide whether and how to offer this feature.
```

### Remove a previous version of an object

*Fedora 4*

```
curl -X DELETE http://localhost:8080/rest/path/to/resource/fcr:versions/<version-name>
```

*Fedora API Spec*

```
Optional: It is up to the implementation to decide whether and how to offer this feature.
```
