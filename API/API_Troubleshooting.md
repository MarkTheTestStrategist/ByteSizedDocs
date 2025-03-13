# API Troubleshooting

### 400 Bad Request

- Are your key values correct :-
	- format
	- length
	- syntax
- Are your keys named correctly :-
	- example:
		- “bodyhtml” should be “bodyHtml”
	- Do you have the right keys in the correct objects?
		- For this, compare with swagger documentation


### 500 Server Error

- When testing locally :-
	- Do you have the correct connection string in your secrets.json file with the correct database name and container name?