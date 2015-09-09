FORMAT: 1A
HOST: https://monsters.kuali.co/api/cm

# KualiCo Curriculum Management

Curriculum management allows faculty and staff of universities to create, manage, review, and propose courses and programs.

Please note that this product under heavy development. Data added may be modified or removed at any time.
<!-- Please only use this for testing & development purposes until the primary release. -->

## Group Authentication

The API can be accessed by including a user's generated API token in the `Authoriation` request header.

After signing into the Kuali Auth service ({yourdomain}.kuali.co/auth), API tokens can be generated and revoked by a user at {yourdomain}.kuali.co/users

Example Request (getting all users):

```
GET https://monsters.kuali.co/api/users?version=1

Headers:
  Authorization: Bearer {token goes here}
```

## Group Versioning

Versioning is coming to all of our resources! For now, only `/users` is versioned. To use a versioned api, you will need to either include a version number on your query string or use the Accept header in your request. See examples below.

### Using the query string

```
GET https://monsters.kuali.co/api/users?version=1

Headers:
  Authorization: Bearer {token goes here}
```

### Using the Accept Header

Note: by using the accept header, you can also request the return type. For now, only json is supported. This is the preferred way to use the API programmatically.

```
GET https://monsters.kuali.co/api/users

Headers:
  Authorization: Bearer {token goes here}
  Accept: vnd.kuali.v1+json
```

## Group Undocumented APIs

Only a handful of our resource APIs are documented here. We have many other resources APIs that we plan on publishing as soon as we are confident in their quality and stability. Those APIs include Workflow, Groups, and Action List among others. We're trying our very hardest to make these APIs production ready as soon as possible and because of this, ***ANY UNDOCUMENTED API IS SUBJECT TO CHANGE WITHOUT NOTICE.*** Use at your own risk.

<!-- include(courses-programs.md) -->

<!-- include(course-program-proposals.md) -->

<!-- include(users.md) -->

<!-- include(options.md) -->
