# Versioning

## Introduction

Fedora 4 provides support for making snapshots of the current state of a resource which in turn become part of the resources version history.  The RDF for historic version snapshots may be browsed and old non-RDF content may be downloaded.  Furthermore, an object or subgraph may be reverted to the state that it existed in a historic version.

The Fedora API Specification supports all the versioning capabilities for Fedora 4, the api for accessing these features will completely change.  To wit, the Fedora API specification conforms to the [Memento](https://mementoweb.org/guide/rfc/) specification.  Memento brings with capabilities that were not available in Fedora 4.  Below we will explore the most vital of these features as well as compare Fedora 4 with the Memento way of doing versioning.

## Overview of the New Memento Hotness

The Memento spec employs some terminology which you may find a bit opaque.  You may find [this diagram](http://mementoweb.org/guide/quick-intro/) helpful in conceptualizing how memento works.  One of the key concepts to grasp is the notion of `TimeGates`.  A `TimeGate` is simply a resource that, when given a date time, will resolve a memento that most closely represents the state of the `resource` on that date.   Instead of having to know the exact date of the memento you wish to retrieve, the `TimeGate` essentially allows you to query the set of mementos for the closest match.  Furthermore the `TimeGate` will return the available time range,  the closest memento, the first and last mementos in the set, and the next and previous mementos relative to the closest match.  So if you wish to move forward or backward in time, you have the information you need.

A related resource is the `TimeMap`.  The `TimeMap` resource returns the set of mementos within a specified time range as well as first and last mementos for the original resource.  In other words,  the `TimeMap`  lets you query the resource for previous versions using a date range.


## Old vs New

### Create a new version

*Fedora 4*
```

curl -H "Slug: <version label>"  -X POST http://localhost:8080/rest/your-resource/fcr:versions

```

*Fedora API Spec*

```
@TODO to be filled in
```

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
@TODO to be filled in
```

### Remove a previous version of an object

*Fedora 4*

```
curl -X DELETE http://localhost:8080/rest/path/to/resource/fcr:versions/<version-name>
```

*Fedora API Spec*

```
@TODO to be filled in
```
