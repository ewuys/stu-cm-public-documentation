## Group Options

Options are used to configure valid values for course and program controls. These are generally used with a Typeahead, 
Dropdown, or Checkbox/Radio group.

Here's what the option schema currently looks like. It's under heavy development, so expect it to change regularly until CM's initial release.

This type notation follows [Facebook's Flow format](http://flowtype.org/).

```
type SettingsOption = {
  id: string;
  type: string; // the type groups options together, for ex. 'Subject Codes'
  name: string; // this the name that appears to users (in controls)
  locale: string; // the same option can be specified in multiple locales
  active: boolean;
}
```

## Existing Options [/options/{id}]

+ Parameters

	+ id (required, string, `fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4`) ... auto-generated option ID

### View [GET]

+ Request

	+ Headers

			X-Token: 'your API key here'

+ Response 200 (application/json)

	+ Body

			{
				"active": true,
				"id": "0a9ccc24-06f9-401c-8fa2-f191db77dbb1",
				"locale": "en-US",
				"name": "Marketing",
				"type": "curricularUnit"
			}

+ Response 404 (text/plain)

	+ Body

			Option not found


### Modify [PUT]

Modify an option by sending a PUT request with the modified JSON representation of the option as the body. The response will return the modified version of the option, or a 404 if no option with that id is found.

+ Request

	+ Headers

			X-Token: 'your API key here'

	+ Body

			{
				"name": "Online Marketing"
			}

+ Response 200 (application/json)

	+ Body

			{
				"active": true,
				"id": "0a9ccc24-06f9-401c-8fa2-f191db77dbb1",
				"locale": "en-US",
				"name": "Online Marketing",
				"type": "curricularUnit"
			}

+ Response 404 (text/plain)

	+ Body

			Option not found

### Inactivate [DELETE]

Options do not support deletion. However, an option can be inactivated by calling this endpoint.

+ Request

	+ Headers

			X-Token: 'your API key here'

+ Response 200 (application/json)

+ Response 404 (text/plain)

	+ Body

			Option not found

## New Options [/options]

### Create a New Option [POST]

Calling this endpoint will create a new option. Note, the type associated with the option may be new as well. Furthermore,
the active and locale fields may be left out. They will default to 'true' and 'en-US' respectively.

+ Request

	+ Headers

			X-Token: 'your API key here'

	+ Body

			{
				"locale": "en-US",
				"name": "Music",
				"type": "jacs"
			}

+ Response 200 (application/json)

	+ Body

			{
				"id": "253e1e5c-1c12-44f1-b9ec-92e5e9964217",
				"active": true,
				"locale": "en-US",
				"name": "Music",
				"type": "jacs"
			}

## Option Types [/options/types]

### Get All Types [GET] 

+ Response 200 (application/json)

	+ Body

			[
				"costcenters",
				"curricularUnit",
				"jacs",
				"org",
				"settings",
				"subject-code",
				"subjectcodes",
				"terms"
			]

## Type Options [/options/types/{type}]

+ Parameters

	+ type (required, string, `jacs`)

### Get All Type Options [GET] 


+ Response 200 (application/json)

	+ Body

			[
				{
				  "active": true,
				  "id": "01f63496-8246-4ee5-8343-680776b4fd58",
				  "locale": "en-US",
				  "longDescription": "Math is for you!",
				  "name": "Math",
				  "shortDescription": "Math",
				  "type": "jacs"
				},
				{
				  "active": false,
				  "id": "1ef88af4-9038-4e78-8cfa-01c8a0d6a336",
				  "locale": "en-US",
				  "type": "jacs"
				},
				{
				  "active": true,
				  "id": "812c2b14-296a-484d-8cda-3086f2c1ec7e",
				  "locale": "en-US",
				  "longDescription": "The study of the application of computer-based technologies.",
				  "name": "I520",
				  "shortDescription": "Bioinformatics",
				  "type": "jacs"
				}
			]
       			