
---
Response
- Time: Verify response time meets performance criteria.
- Code: Confirm the HTTP status code is correct.
- Status: Check that the response status/message is as expected.
---
JSON Request Body
- Extra (Ghost) Keys/Values:
	- Include extra keys/values and verify they are accepted but ignored.
- No Body:
	- Send an empty body and expect a 400 Bad Request.
- Missing Mandatory Keys/Values:
	- Omit required keys and expect a 400 Bad Request.
- Only Mandatory Keys:
	- Send only required keys/values and verify proper processing.
- IDs:
	- Use the same ID for all ID fields if required by the contract.
---
Key Values
- Length Validation:
	- Verify minimum and maximum lengths.
	- For IDs with fixed lengths, change the format while keeping the length.
- Blank Strings:
	- Test with empty strings (e.g., "") to see how they are handled.
---
Parameters
- Page Size:
	- Determine the maximum allowed value.
	- Test values within and outside the allowed range.
- Page Number:
	- Confirm the minimum is 0 and validate upper limits and negative values.
- Ghost Values:
	- Provide extra key-value pairs to ensure they’re ignored.
- SortBy:
	- Test sort orders (ascending, descending, relevance).
	- Verify sorting works correctly for names with different cases, symbols, or numbers.
---
URL
- Malformed URLs:
	- Test with incorrect URLs or IDs embedded in the URL.
- Spaces:
	- Ensure that URLs with spaces are handled correctly.
---
Pagination
- Boundary Values:
	- Negative numbers, exact minimum, exact maximum, and exceeding maximum values.
	- Decimal numbers and excessively long numeric values.
---
Authentication
- Refresh Token:
	- Valid refresh token.
	- Expired refresh token.
	- Request without a refresh token.
	- Invalid refresh token.
- Access Token:
	- Verify required fields are present (iat, exp, nbf, iss, alg, typ).
	- Test with invalid and expired tokens.
---
Authentication Types
- Basic Authorization (username/password).
- Bearer Token (OAuth 2.0).
- API Key.
---
Search Endpoints
- Single words.
- Multiple words with spaces.
- Spaces before and after the search terms.
---
Email Addresses
- Validate correct syntax (e.g., minimal valid: a@a.uk).
- Test with spaces before, after, and within the email.
---
Telephone Numbers
- Maximum of 11 characters.
- Handling of spaces, plus sign (+), and brackets (e.g., UK format).
---
Duplication
- Verify whether duplicate records can be added.
---
Arrays
- Validate the minimum and maximum number of items.
- Ensure each item is of the correct data type.
---
Boolean
- Accept only true or false values.
---
Text
- Test with mixed casing, alphabetic, alphanumeric characters.
- Include symbols, Kanji, umlauts.
- Check handling of HTML and JavaScript content.
---
Dates
- Validate the implemented date format.
- Test alternative formats (e.g., ISO 8601).
- Remove parts of the ISO date (time zone, time, or date) and verify behavior.
---
Colour
- Validate hexadecimal color codes (max 9 characters: one hash + 8 digits).
---
Methods
- Change the HTTP method (e.g., to PUT/DELETE on a GET-only endpoint) to expect a 405 Method Not Allowed.
---
Contract Verification
- Request:
	- Send all allowed properties with values and verify that the response contains the expected data.
- Schema:
	- Validate that the JSON/XML response adheres to the defined schema, including required fields and data types.
---
Response Body
- Ensure the returned JSON/XML is formatted correctly.
- Confirm that all expected properties and values are present.
---
Error Messages
- Ensure error messages are clear, descriptive, and provide actionable guidance when issues occur.
- Confirm that similar error scenarios produce consistent messages across the API.
---
Headers
- Request Headers:
	- Verify that all required request headers (e.g., Content-Type, Accept, Authorization) are present and correctly formatted.
- Response Headers:
	- Ensure responses include expected headers such as Cache-Control, X-Correlation-ID, or custom headers defined in the contract.
---
Rate Limiting & Throttling
- Verify that when the API is hit with excessive requests, it returns a 429 Too Many Requests status.
- Check that any rate limit headers (if provided) correctly indicate the remaining quota and reset time.
---
Idempotency
- For safe and repeatable operations (e.g., GET, PUT, DELETE), test that repeated requests produce consistent results.
- Validate that endpoints marked as idempotent in the contract behave accordingly when the same request is sent multiple times.
---
CORS (Cross-Origin Resource Sharing)
- Confirm that the API returns the proper CORS headers (e.g., Access-Control-Allow-Origin) when accessed from different origins.
- Test scenarios with various origins to ensure cross-domain requests are handled as specified.
---
