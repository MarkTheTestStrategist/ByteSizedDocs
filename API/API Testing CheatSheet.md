Response

- Time
- Code
- Status


JSON Body

- Add ghost keys and values
	- Accepted just ignored
- Send request with no body
	- 400 bad request should be returned
- Remove Mandatory keys & values
	- 400 bad request
- Send request with only mandatory keys & values
- Id's
	- Use the same id for all id requirements where the id is different.


Key Values

- Min Length
- Max Length
- Where it is an ID with a specific length, change the format but keep the same length
- Leave strings blank : ""


Parameters

- Page Size
	- What is the max page size?
	- Test between the min and max sizes
	- Test outside the min and max sizes
- Page
	- What is the maximum page number?
	- Minimum will start at zero
	- Test between minimum and maximum
	- Test minus values
- Ghost Values
	- Example: -
		- Key: Something
		- Value: Something
- SortBY
	- Asc
	- Desc
	- Relevance
	- Check where names start with caps and those with lowercase are being sorted correctly.
	- Check where names begin with symbols or numbers are being sorted correctly.


URL

- Incorrect URL
- Incorrect id's where id's are included in the URL
- Spaces in the URL


Pagination

- Minus values
- Exact minimum value
- Exact maximum value
- Exceed maximum value
- Value with decimal point
- A very long value


Authentication

- Refresh Token
	- Try to refresh token when valid
	- Try to refresh token when expired
	- Submit request without refresh token present
	- Submit request with an invalid token
- Access Token
	- Check all values are present in the token
		- Examples:
			- iat = issued at
			- exp = expiry time
			- nbf = not valid before
			- iss = Issuer. Who created and signed this token
			- alg = encryption or signature algorithm
			- typ = Type of token e.g. Bearer
	- Try with an invalid token
	- Try with an expired token


Search Endpoints

- Enter single words
- Enter words with spaces
- Add spaces before and after words


Email Addresses

- Validation
	- correct syntax, so minimum would be a@a.uk
	- enter space before and after email
	- enter space within email


Telephone Numbers

- Max 11 Chars
- spaces
- Plus Sign +
- Brackets (UK)


Duplication

- Can the same record be added again


Arrays

- Min Items
- Max Items
- Item types


Boolean

- can only be true or false


Text

- Mixed Casing
- Alphabetic
- Alphanumeric
- Symbols
- Kanji
- Umlauts
- HTML
- JavaScript


Dates

- Validate the implemented date format
- Use other date formats such as...
	- ISO 8601
- Remove the time zone & keep the rest from the ISO date format
- Remove the time from & keep the rest from the ISO date format
- Remove the date from & keep the rest from the ISO date format


Colour

- Max hexacode is 9 (8 digits and one hash)


Security Tests

- SQL Injection: Try entering SQL commands in text fields.
- XSS (Cross-Site Scripting): Input <script>alert('XSS')</script> in request parameters.
- Authentication Bypass: Try accessing protected endpoints without authentication.
- Rate Limiting: Send a high volume of requests to check API throttling.


Performance Tests

- Load Testing: Simulate high user load and measure response time.
- Stress Testing: Overload the API to determine breaking points.
- Spike Testing: Send traffic spikes to observe system stability.


Negative Testing

- Incorrect Content-Type: Send requests with an unsupported Content-Type.
- Large Payloads: Test with excessively large request bodies.
- Special Characters: Include emojis, accents, and Unicode characters.
- Empty Headers: Remove essential headers and test API behavior.


Integration & Contract Testing

- Dependency Failures: Simulate failures in third-party services.
- Backward Compatibility: Ensure old API versions still work after updates.

