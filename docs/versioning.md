# Versioning

## Introduction

The Fedora API specification conforms to the [Memento](https://mementoweb.org/guide/rfc/) specification.  Memento brings with it all the versioning capabilities of Fedora 4 along with some new features. Below we will explore the most vital of these new features as well as compare the Fedora 4 with the Memento way of doing versioning.

## Overview of the New Memento Hotness

The Memento specification makes use of a handful of essential concepts.  You may find [this diagram](http://mementoweb.org/guide/quick-intro/) helpful in gaining an overall understanding of how Memento works.  One of the key concepts to grasp is the notion of `TimeGates`.  A `TimeGate` is simply a resource that, when given a date time, will resolve a memento that most closely represents the state of the `resource` on that date.   Instead of having to know the exact date of the memento you wish to retrieve, the `TimeGate` essentially allows you to query the set of mementos for the closest match.  Furthermore the `TimeGate` will return the available time range,  the closest memento, the first and last mementos in the set, and the next and previous mementos relative to the closest match.  So if you wish to move forward or backward in time, you have the information you need.

A related resource is the `TimeMap`.  The `TimeMap` resource returns the set of mementos within a specified time range as well as first and last mementos for the original resource.  In other words,  the `TimeMap`  lets you query the resource for previous versions using a date range.


## Old vs New

### Version Creation 

While Fedora 4  supports client controlled version creation, the Fedora API Spec defines this behavior as optional.  Instead, it is up to the 
implementation to decide whether versioning is client and/or server managed.


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
