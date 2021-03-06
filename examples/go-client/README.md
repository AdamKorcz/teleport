## Teleport Auth Go Client

### Introduction

Teleport Auth Server has an API which hasn't been officially documented (yet).
Both `tctl` and `tsh` use the Auth API to perform various actions

This program demonstrates how to...

1. Authenticate against the Auth API using certificates.
2. Make API calls to issue CRUD requests for cluster join tokens, roles, and labels.
3. Receive, allow, and deny access requests.

### API Authentication

Auth API clients must perform two-way authentication using x509 certificates:

1. They have to validate the auth server x509 certificate to make sure the
   API endpoint can be trusted.
2. They must offer their x509 certificate, which has been previously issued
   by the auth sever.

Start up a teleport auth server and then run the following commands to create an `api-user` with a signed certificate. Make sure to run this from the `go-client` directory for proper output.

```bash
$ tctl create -f api-user-role.yaml
$ mkdir -p certs
$ tctl auth sign --format=tls --ttl=87600h --user=api-user --out=certs/api-user
```

### Demo

With the user and certificate created, you can run the go example.

```bash
$ go run .
```

### TODO

Turn this example into a seperate repository (or git/go submodule if that has the same effect), so that users can quickly clone it and run it without worrying about dependencies.

Replace Upsert with Create/Update once these are implemented. (update docs as well)

We need to add a snippet on how to enumerate trusted clusters and connect to their API endpoints later.
