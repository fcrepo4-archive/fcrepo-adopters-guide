# Versioning

## Introduction

Fedora 4 provides support for making snapshots of the current state of a resource which in turn become part of the resources version history.  The RDF for historic version snapshots may be browsed and old non-RDF content may be downloaded.  Furthermore, an object or subgraph may be reverted to the state that it existed in a historic version.

The Fedora API Specification supports all the versioning capabilities for Fedora 4, the api for accessing these features will completely change.  To wit, the Fedora API specifcation conforms to the [Memento](https://mementoweb.org/guide/rfc/) specification.  Memento brings with capabilities that were not available in Fedora 4.  Below we will explore the most vital of these features as well as compare Fedora 4 with the Memento way of doing versioning.

## Overview of the New Memento Hotness


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
