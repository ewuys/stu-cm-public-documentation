## Group Users

# NOTE: User's have been removed from CM and are now stored in a centralized service. Any calls to `/users` must not contain the `/cm` prefix but they must contain a version query param. i.e.: `GET monsters.kuali.co/api/users?version=1`

Here's what the user schema currently looks like. It's under heavy development, so expect it to change regularly until CM's initial release.

This type notation follows [Facebook's Flow format](http://flowtype.org/).

```
type User = {
  id: string;
  name: string;
  username: string;
  email: string;
  password?: string; // This can be set in a PUT or POST request, but it's not query-able.
  role: 'admin' | 'user';
  created_at: DateString;
  updated_at: DateString;
}
```

## Existing Users [/users/{id}]

+ Parameters

	+ id (required, string, `fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4`) ... auto-generated course ID

### View [GET]

+ Request

	+ Headers

			X-Token: 'your API key here'

+ Response 200 (application/json)

	+ Body

			{
				"created": 1429163259579 ,
				"department":  "Practical Research in Child-based Energy" ,
				"email": 'sully@monsters.edu',
				"id":  "153a4970-f75d-4ba5-92a9-18829411fff0" ,
				"role":  "admin" ,
				"username":  "Sully"
			}

+ Response 404 (text/plain)

	+ Body

			Course not found


### Modify [PUT]

Modify a user by sending a PUT request with the modified JSON representation of the user as the body. The response will return the modified version of the user, or a 404 if no user with that id is found.

+ Request

	+ Headers

			X-Token: 'your API key here'

	+ Body

			{
				"department":  "Closet Camouflage Research" ,
				"username":  "JamesPSullivan",
				"password": "AVerySecurePassword"
			}

+ Response 200 (application/json)

	+ Body

			{
				"created": 1429163259579 ,
				"department":  "Closet Camouflage Research" ,
				"email": 'sully@monsters.edu',
				"id":  "153a4970-f75d-4ba5-92a9-18829411fff0" ,
				"role":  "admin" ,
				"username":  "JamesPSullivan"
			}

+ Response 404 (text/plain)

	+ Body

			Course not found

### Remove [DELETE]

Calling this endpoint will delete a user.

**CAVEAT**: this endpoint will be removed soon. Ultimately users will not be able to be removed through the API, only marked as inactive.

+ Request

	+ Headers

			X-Token: 'your API key here'

+ Response 200

+ Response 404 (text/plain)

	+ Body

			User not found

## New Users & Multiple Users [/users]

### Create a New User [POST]

+ Request

	+ Headers

			X-Token: 'your API key here'

	+ Body

			{
				"department":  "Dept. for the Specialties of Short Scarers" ,
				"email": 'mike@monsters.edu',
				"role":  "user" ,
				"username":  "Mike",
				"password": "Celia"
			}

+ Response 200 (application/json)

	+ Body

			{
				"id":  "9f289c2a-ad6d-4b70-8da7-54ea22a2e5c0" ,
				"department":  "Dept. for the Specialties of Short Scarers" ,
				"email": 'mike@monsters.edu',
				"role":  "user" ,
				"username":  "Mike",
				"password": "Celia"
			}

### View Multiple Users [GET]

**CAVEAT:** Pagination isn't implemented yet, but it's coming!

+ Response 200 (application/json)

	+ Body

			[
				{
					"created": 1429163259579 ,
					"department":  "Closet Camouflage Research" ,
					"email": 'sully@monsters.edu',
					"id":  "153a4970-f75d-4ba5-92a9-18829411fff0" ,
					"role":  "admin" ,
					"username":  "JamesPSullivan"
				},
				{
					"created": 1429163858271 ,
					"department":  "Dept. for the Specialties of Short Scarers" ,
					"email": 'mike@monsters.edu',
					"id":  "9f289c2a-ad6d-4b70-8da7-54ea22a2e5c0" ,
					"role":  "user" ,
					"username":  "Mike",
				}
			]
