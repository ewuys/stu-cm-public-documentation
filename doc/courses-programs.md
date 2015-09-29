## Group Courses and Programs

**This section addresses API routes that deal with courses or programs. The docs use the example of courses, but anything done to courses can be done to programs by changing the URL to /programs/ instead of /courses/**

The schema for a course is almost completely dynamic. There are a few required attributes that we use to make the app work, but most of the fields on a form will be configured at run-time through a web interface on a per-university basis.

See [Course Schema](#courses-course-schema) for more information

## Course Schema [/courses/schema]

This endpoint returns an object with keys representing all of the attributes that are currently settable
or gettable on a course.

Each key on the schema object contains information surrounding a course attribute.

Here's an example of what a schema might look like:

---

```
{
	regOptions: {
		label: "Student Registration Options",
		options: [
			{
				key: "audit",
				text: "Audit"
			},
			{
				key: "passFail",
				text: "Transcript Pass/Fail"
			}
		],
		type: "Checkboxes"
	},
	...
}
```
---

`regOptions` corresponds to the API labels given when the gadget was created. `regOptions` is a `checkboxes` gadget with two options: `Audit` and `Transcript Pass/Fail`.

## View [GET]

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				"number": {
					"label": "Number",
					"limit": "5"
				},
				...
			}

## Course Schema Attribute [/courses/schema/{key}]

+ Parameters

	+ key (required, string, 'number') ... Schema attribute key

## View [GET]

Assuming we didn't want to fetch the entire schema for the course, but one specific attribute,
we can add the key for that attribute onto the end of the path.

In this example we're sending a GET request to `/courses/schema/number`

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				"label": "Number",
				"limit": "5"
			}

## Dependencies [/courses/dependencies/{id}]

## View [GET]

Returns an array containing partial program objects upon which the requested course is dependent. (i.e. completion requirements, entrance requirements, satisfactory progress)

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			[{
				{
					id: "7a7bdd8a-9f59-4608-8ce5-742dc539827c"
					code: "TSAMTMBS"
					title: "Aeronautical Management Technology (Air Transportation Management)"
					rules: {
						rules:
							{
								alphaCharacter: "A"
								courses:
									0: "8e080369-15c2-4338-9f21-fcd4ab00fa20"
									1: "077ffb34-44f1-478f-9d9c-790f5c85b671"
									2: "41364606-ed3b-4502-8deb-443ba86c5bfd"
									3: "dbefeabb-b243-4412-896d-76381c235015"
									4: "c994ed42-d188-4834-9611-d67cc872ec2d"
									id: "Vy6zDA2"
									isRuleSet: false
									minCredits: "2"
									subType: "coursesNumber"
									type: "numberCourses"
							}
					}
					lbl: "Entrance Requirements"
					type: "programs"
				}
				{
					...
				}
				...
			}]

## Existing Courses [/courses/{id}{?includeSchema}]

+ Parameters

	+ id (required, string, `fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4`) ... auto-generated course ID

+ Parameters

	+ includeSchema (boolean, optional) - Render the course schema inline with the values for this course.
		+ Default: `false`

### View [GET]

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				"id": "fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4",
				"title": "Disappearing & Hiding",
				"subjectCode": "SCAR",
				"number": "201A",
				...
			}

+ Response 404 (text/plain)

	+ Body

			Course not found


### Modify [PUT]

Modify a course by sending a PUT request with the modified JSON representation of the course as the body. The response will return the modified version of the course, or a 404 if no course with that id is found.

**Note:** Invalid courses will be saved. When this happens, errors will come back under `validations`.

+ Request

	+ Headers

			X-Token: 'your API key here'

	+ Body

			{
				"title": "Disappearing & Hiding, Modified",
			}

+ Response 200 (application/json)

	+ Body

			{
				"id": "fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4",
				"title": "Disappearing & Hiding, Modified",
				"subjectCode": "SCAR",
				"number": "201A",
				...
				"validations": "{error object}"
			}

+ Response 404 (text/plain)

	+ Body

			Course not found


## Versions [/courses/{pid}/versions]

### View [GET]

Return an array containing all versions of a course with the newest version at index 0.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				[
					{
						approvalDate: 192380175910
						created: 1923850150198
						createdBy: 012981dd-0192-df9e-90fe-098209840aff
						description: "This course has multiple versions! v2.0"
						...
					}
					{
						approvalDate: 1923800000
						created: 1923850150198
						createdBy: 012981dd-0192-df9e-90fe-098209840aff
						description: "This course has multiple versions! v1.0"
					}
					...
				]
			}

+ Response 404 (text/plain)

	+ Body

			Course not found

## Latest Active Version [/courses/{pid}/latestActive]

### View [GET]

Return the course object of the active version of the requested pid.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				approvalDate: 1439246948928
				created: 1439246774300
				createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
				description: "Now it has a description because the 2016 budget allowed it."
				...
			}

+ Response 404 (text/plain)

	+ Body

			Course not found

## Proposal in Review [/courses/{pid}/review]

### View [GET]

Returns the course object of the proposed draft that is currently being reviewed in workflow but has not been approved yet.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			{
				approvalDate: 1439310941443
				created: 1439311325358
				createdBy: "711a841f-8e90-4f1d-8274-97575221bd8f"
				description: "Now it has a description because the 2016 budget allowed it."
				...
				status: "review"
			}

## Shared Proposals [/courses/{pid}/sharedWithMe]

### View [GET]

Returns an array of the course proposals for the pid that have been shared with the user by whom the API key was created.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

			[
				{
					creator: "John Smith"
					itemId: "be073f44-2e9c-4b51-87c8-8e6c3fe325fa"
				}
				...
			]

## Clone Course [/courses/{id}]

### Clone Course [POST]

Makes a proposal from the course from the course with the given id, and returns the newly cloned proposal object.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

	{
		approvalDate: 1439311761735
		created: 1439315226880
		createdBy: "711a841f-8e90-4f1d-8274-97575221bd8f"
		id: "25c2d6c5-d297-463d-aaa2-db9b69a160e8"
		originalProposalId: "4b1be7ca-4f47-488d-b393-9aa5986abd1c"
		pid: "VkB2qxGs"
		proposedFromId: "8e738178-c009-45df-81a2-093d2f030e77"
	}

## Start Dates [/courses/startdates/{pid}]

### Verify Uniqueness [POST]

Verifies the uniqueness of a start date between versions of a pid. Returns a boolean 'unique' with value true if the date specified in the body of the request is not equal to the start date of any version of the course.

+ Request

	+ Headers

			X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

	{
		unique: false
	}

## Retire Courses [/courses/{id}/retire]

### Retire Course [PUT]

Retires the course with given id, assuming the API key is associated with a user that has admin permissions. Returns the retired course object.

+ Request

	+ Headers

		X-Token: '{your API key here}'

	+ Body

		endDate: {
			type: 'year',
			year: '2015'
		},
		rationale: 'Retire rationale here'

+ Response 200 (application/json)

	+ Body

	{
		approvalDate: 1439311761735
		created: 1439311868900
		createdBy: "711a841f-8e90-4f1d-8274-97575221bd8f"
		endDate: {
			type: "year"
			year: "2015"
		}
		id: "212c19be-1088-40c9-aacc-ebe15e1a83c8"
		originalProposalId: "4b1be7ca-4f47-488d-b393-9aa5986abd1c"
		pid: "VkB2qxGs"
		proposedFromId: "8e738178-c009-45df-81a2-093d2f030e77"
		rationale: "Retire rationale here"
		**status: "retired"**
		...
	}

## Share Proposals [/courses/{id}/sharing]

### Share Proposal [PUT]

Share the proposal with the users in the passed in with the request body.

+ Request

	+ Headers

		X-Token: '{your API key here}'

	+ Body

		[
			{
				id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
				name: "admin"
			}
			...
		]

+ Response 200 (application/json)

	+ Body

	{
		created: 1439321912784
		createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
		department: "Vy8d5Of9"
		...
		sharedWith:[
			{
				id: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
				name: "admin"
			}
		]
		...
	}

## Submit for Approval [/courses/{id}/submitForApproval]

### Submit [POST]

Submits the given proposal id for approval via workflow.

+ Request

	+ Headers

		X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

	{
		created: 1439321912784
		createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
		...
		description: "API TESTING COURSE!"
		id: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
		...
		pid: "41YL04Qs"
		proposalRationale: "Making a new thing"
		...
		status: "review"
		...
		workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		possibleUserActions: [
			"edit",
			"withdraw"
		]
	}

## Approve in Workflow [/courses/{id}/approve]

### Approve [POST]

Approve the item in workflow, assuming it is pending the decision of the user associated with the API key.

+ Request

	+ Headers

		X-Token: '{your API key here}'

	+ Body

		comment: 'Looks great!'

+ Response 200 (application/json)

	+ Body

	{
		created: 1439321912784
		createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
		...
		description: "API TESTING COURSE!"
		id: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
		...
		pid: "41YL04Qs"
		proposalRationale: "Making a new thing"
		...
		status: "active"
		...
		workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		possibleUserActions: [
			"edit"
		]
	}

## Reject in Workflow [/courses/{id}/reject]

### Reject [POST]

Reject the item in workflow, assuming it is pending the decision of the user associated with the API key.

+ Request

	+ Headers

		X-Token: '{your API key here}'

	+ Body

		comment: 'Change the description to be more accurate'

+ Response 200 (application/json)

	+ Body

	{
		created: 1439321912784
		createdBy: "1366763d-35d2-462b-b7d9-b3ffef07b78f"
		...
		description: "API TESTING COURSE!"
		id: "fc061d1c-fdc5-4d98-b5c1-3981d139f37a"
		...
		pid: "41YL04Qs"
		proposalRationale: "Making a new thing"
		...
		status: "review"
		...
		workflowId: "ce7fd5f8-1960-436b-aef7-899f0b9e64bd"
		possibleUserActions: [
			"edit"
		]
	}


## Course Config [/courses/template/body]

### View [GET]

Get the course config page that defines what information gadgets are shown on the course view and edit pages. The schema is as follows: `template` contains children of type `panel`, which contain children of type `row`, which contain children of type `column`, which contain the individual gadgets.

+ Request

	+ Headers

		X-Token: '{your API key here}'

+ Response 200 (application/json)

	+ Body

		{
			id: "course-template"
			template: [
				{
					children: [
						{
							children: [
								{
									children: [
										{
											descriptiveText: "Workflow Viewer"
											gKey: "workflowviewer"
											label: "workflowViewer"
											type: "WorkflowViewer"
										}
										...
									],
									type: "Column"
								}
								...
							],
							type: "Row"
						}
						...
					]
					label: "General Information"
					type: "panel"
				}
			]
		}

### Modify [PUT]

**NOT SUPPORTED YET**

## New Courses & Multiple Courses [/courses]

### Create a new course [POST]

Add a course.

**CAVEAT:** As of right now, courses must include the 'startTerm' and 'status' attributes or they will not show up in the course search page.

Set 'status' to 'draft' to make it a proposal

+ Request

	+ Headers

			X-Token: '{your API key here}'

	+ Body

			{
				"title": "Tactics for Scary Napping",
				"subjectCode": "NAPS",
				"number": "400"
				"startTerm": {
					"type":"year"
					"year":2015
				}
				"status":"active"
			}

+ Response 200 (application/json)

	+ Body

			{
				"id": "92062dcf-d975-4e57-8073-03f202082786",
				"title": "Tactics for Scary Napping",
				"subjectCode": "NAPS",
				"number": "400"
			}

### View multiple courses [GET]

Return a list of all course proposals, regardless of approval status.

**CAVEAT:** Pagination isn't implemented yet, but it's coming!

+ Response 200 (application/json)

	+ Body

			[
				{
					"id": "fa2ef9e1-1ca2-4acb-a4b0-1b87ea4026a4"
					"title": "How to look scary while eating lunch",
					"subjectCode": "LUNCH",
					"number": "109"
				},
				{
					"id": "197b85ee-3c1a-4933-87fa-a4567da82dc1"
					"title": "Pre-scare self-uglification",
					"subjectCode": "SCAR",
					"number": "242"
				},
				{
					"id": "92062dcf-d975-4e57-8073-03f202082786",
					"title": "Tactics for Scary Napping",
					"subjectCode": "NAPS",
					"number": "400"
				}
			]
