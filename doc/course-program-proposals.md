## Group Proposals

**This section addresses API routes that deal with proposals for courses or programs. The docs use the example of courses, but anything done to courses can be done to programs by changing the URL to /proposals/programs/ instead of /proposals/courses/**

## Proposals [/proposals/courses/]

### View Current Proposals [GET]

Return an array containing the proposals created by the user with which the API key is associated.

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		[
			{
				approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
				created: 1439326621386
				createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
				department: "Vy8d5Of9"
				description: "API TESTING COURSE!"
				id: "556331c7-4c54-4e85-885b-fbce687d80ba"
				meta: {
					proposalType: "create"
				}
				number: "999"
				pid: "41YL04Qs"
				proposalRationale: "Making a new thing"
				sharedWith: [
					{
						id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
						name: "admin"
					}
				]
				startTerm: {
					month: "January"
					type: "month"
					year: "2015"
				}
				status: "approved"
				subjectCode: "API"
				title: "API Testing"
				updated: 1439324556337
				workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
			},
			...
		]

+ Response 404 (text/plain)

	+ Body

			Proposal not found

### Create Proposal [POST]

Create a new proposal with the details sent in the body of the request.

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		{
			approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
			created: 1439326621386
			createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
			department: "Vy8d5Of9"
			description: "API TESTING COURSE!"
			id: "556331c7-4c54-4e85-885b-fbce687d80ba"
			meta: {
				proposalType: "create"
			}
			number: "999"
			pid: "41YL04Qs"
			proposalRationale: "Making a new thing"
			sharedWith: [
				{
					id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
					name: "admin"
				}
			]
			startTerm: {
				month: "January"
				type: "month"
				year: "2015"
			}
			status: "approved"
			subjectCode: "API"
			title: "API Testing"
			updated: 1439324556337
			workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		}

+ Response 404 (text/plain)

	+ Body

			Proposal not found

## Existing Proposals By ID [/proposals/courses/{id}]

### View [GET]

Return proposal with given ID.

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		{
			approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
			created: 1439326621386
			createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
			department: "Vy8d5Of9"
			description: "API TESTING COURSE!"
			id: "556331c7-4c54-4e85-885b-fbce687d80ba"
			meta: {
				proposalType: "create"
			}
			number: "999"
			pid: "41YL04Qs"
			proposalRationale: "Making a new thing"
			sharedWith: [
				{
					id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
					name: "admin"
				}
			]
			startTerm: {
				month: "January"
				type: "month"
				year: "2015"
			}
			status: "approved"
			subjectCode: "API"
			title: "API Testing"
			updated: 1439324556337
			workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		}

+ Response 404 (text/plain)

	+ Body

			Proposal not found

### Modify [PUT]

Change proposal with a given ID.

+ Request

	+ Headers

		X-Token: '{your api key here}'

	+ Body

		{
			description: "API TESTING COURSE! Modified"
		}

+ Response 200

	+ Body

		{
			approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
			created: 1439326621386
			createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
			department: "Vy8d5Of9"
			description: "API TESTING COURSE! Modified"
			id: "556331c7-4c54-4e85-885b-fbce687d80ba"
			meta: {
				proposalType: "create"
			}
			number: "999"
			pid: "41YL04Qs"
			proposalRationale: "Making a new thing"
			sharedWith: [
				{
					id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
					name: "admin"
				}
			]
			startTerm: {
				month: "January"
				type: "month"
				year: "2015"
			}
			status: "approved"
			subjectCode: "API"
			title: "API Testing"
			updated: 1439324556337
			workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		}

+ Response 404 (text/plain)

	+ Body

			Proposal not found

### Clone [POST]

Make a new proposal based off of the proposal with given ID.

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		{
			approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
			created: 1439326621386
			createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
			department: "Vy8d5Of9"
			description: "API TESTING COURSE!"
			id: "556331c7-4c54-4e85-885b-fbce687d80ba"
			meta: {
				proposalType: "modify"
			}
			number: "999"
			pid: "41YL04Qs"
			proposalRationale: "Making a new thing"
			proposedFromId: "dc0b1626-e587-4426-8b12-d1b6091e58bf"
			sharedWith: [
				{
					id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
					name: "admin"
				}
			]
			startTerm: {
				month: "January"
				type: "month"
				year: "2015"
			}
			status: "draft"
			subjectCode: "API"
			title: "API Testing"
			updated: 1439324556337
			workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		}

+ Response 404 (text/plain)

	+ Body

		Proposal not found

### Delete [DELETE]

Deletes the proposal with the specified ID.

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		OK

+ Response 404 (text/plain)

	+ Body

			Proposal not found

## Proposal Status [/proposals/courses/{status}/{id}]


### Modify [PUT]

# This will override the workflow process. We strongly recommended that you don't ever use this.

---

Modify the status of a proposal with id {id}. Status will be set as {status}.

+ Parameters

	+ id (required, string, `fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4`) ... auto-generated course ID

	+ status (required, string, `approved`)

+ Request

	+ Headers

		X-Token: '{your api key here}'

+ Response 200

	+ Body

		{
			approvedVersionId: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
			created: 1439326621386
			createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
			department: "Vy8d5Of9"
			description: "API TESTING COURSE!"
			id: "556331c7-4c54-4e85-885b-fbce687d80ba"
			meta: {
				proposalType: "modify"
			}
			number: "999"
			pid: "41YL04Qs"
			proposalRationale: "Making a new thing"
			proposedFromId: "dc0b1626-e587-4426-8b12-d1b6091e58bf"
			sharedWith: [
				{
					id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
					name: "admin"
				}
			]
			startTerm: {
				month: "January"
				type: "month"
				year: "2015"
			}
			status: "active"
			subjectCode: "API"
			title: "API Testing"
			updated: 1439324556337
		}

+ Response 404 (text/plain)

	+ Body

			Proposal not found
