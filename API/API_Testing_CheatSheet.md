# API Testing Cheat-Sheet

## Overview

This cheat-sheet is designed to serve as a quick reference guide for testing API endpoint contracts. It covers everything from validating response codes, status, and performance metrics to ensuring that request bodies, headers, parameters, and URLs conform to the defined specifications. It also addresses more advanced aspects like authentication, rate limiting, idempotency, and CORS, while detailing best practices for handling edge cases in data types such as text, dates, and color codes. Use this guide to ensure consistent, reliable, and secure API behavior across all scenarios.

---

### 1. Response

- Time:
	- Verify that the response time meets performance criteria.
- Code:
	- Confirm the HTTP status code is correct.
		- Examples:
			- 200 OK: Request was successful (e.g., GET returns data).
			- 201 Created: A new resource was successfully created (e.g., POST).
			- 400 Bad Request: The request is malformed, missing mandatory fields, or contains invalid values.
			- 401 Unauthorized / 403 Forbidden: Authentication failed or the client does not have permission.
			- 404 Not Found: The requested resource does not exist.
			- 405 Method Not Allowed: An unsupported HTTP method was used (e.g., PUT on a GET-only endpoint).
			- 409 Conflict: A duplicate record or conflicting data exists.
			- 429 Too Many Requests: Rate limiting has been triggered.
			- 500 Internal Server Error: An unexpected error occurred on the server.
			- 501 Not Implemented: The server does not support the requested functionality.
- Status Message:
	- Verify that the response status/message is as expected.
---

### 2. JSON Request Body

- Extra (Ghost) Keys/Values:
	- Include additional keys/values and verify they are accepted but ignored by the API.
- No Body:
	- Send an empty body and expect a 400 Bad Request.
- Missing Mandatory Keys/Values:
	- Omit required keys and expect a 400 Bad Request.
- Only Mandatory Keys:
	- Send only the required keys/values and verify proper processing.
- IDs:
	- When the contract requires it, use the same ID for all ID fields.
---

### 3. Key Values

- Length Validation:
	- Verify minimum and maximum allowed lengths.
	- For IDs with fixed lengths, alter the format (if applicable) while maintaining the required length.
- Blank Strings:
	- Test with empty strings (e.g., "") and observe how they are handled.
---

### 4. Parameters

- Page Size:
	- Determine and test the maximum allowed page size, as well as values within and outside the allowed range.
- Page Number:
	- Confirm the minimum is 0; test for upper limits and negative values.
- Ghost Values:
	- Provide extra key-value pairs to ensure they are ignored.
- SortBy:
	- Test sorting in ascending, descending, and relevance orders.
	- Validate sorting for names containing different cases, symbols, or numbers.
---

### 5. URL

- Malformed URLs:
	- Test with incorrect URL formats or with invalid IDs embedded in the URL.
- Spaces:
	- Ensure that URLs containing spaces are properly handled (encoded if necessary).
---

### 6. Pagination

- Boundary Values:
	- Test with negative numbers, the exact minimum, the exact maximum, and values exceeding the maximum.
	- Also test with decimal numbers and overly long numeric values.
---

### 7. Authentication

- Refresh Token:
	- Valid refresh token: Ensure processing works as expected.
	- Expired refresh token: Expect an appropriate error (e.g., 401 Unauthorized).
	- No refresh token: Validate that the request is rejected.
	- Invalid refresh token: Check for error handling.
- Access Token:
	- Verify that required fields (e.g., iat, exp, nbf, iss, alg, typ) are present.
	- Test with invalid or expired tokens.
---

### 8. Authentication Types

- Basic Authorization:
	- Test using username/password.
- Bearer Token:
	- Validate OAuth 2.0 token scenarios.
- API Key:
	- Ensure proper API key handling.
---

### 9. Search Endpoints

- Search Terms:
	- Single words, multiple words with spaces, and terms with leading/trailing spaces.
---

### 10. Email Addresses

- Syntax Validation:
	- Verify the correct format (e.g., minimal valid: a@a.uk).
	- Test with spaces before, after, and within the email address.
---

### 11. Telephone Numbers

- General Rules:
	- Validate a maximum of 11 characters (adjust as per the API's specific contract).
- Formatting:
	- Test handling of spaces, plus signs (+), and brackets.
- Country-Specific Examples:
	- UK: Phone numbers should typically start with +44 followed by the national number (e.g., +44 20 7946 0958).
	- China: Validate numbers starting with +86 and follow local formatting conventions (e.g., +86 10 1234 5678).
---

### 12. Duplication

- Record Duplication:
	- Verify whether duplicate records can be added, and ensure the API returns a proper error (e.g., 409 Conflict) if duplicates are not allowed.
---

### 13. Arrays

- Item Count:
	- Validate the minimum and maximum number of items.
	- Ensure each item in the array is of the correct data type.
---

### 14. Boolean

- Validation:
	- Accept only true or false values. Test that any other values are rejected.
---

### 15. Text

- Input Variety:
	- Test with mixed casing, alphabetic, and alphanumeric characters.
	- Include symbols, Kanji, umlauts, etc.
	- Check how HTML and JavaScript content are handled.
---

### 16. Dates

- Date Format:
	- Validate that dates conform to the implemented format (e.g., ISO 8601).
	- Test alternative formats and partial dates (omitting time zone, time, or date components) to verify behavior.
---

### 17. Colour

- Hexadecimal Codes:
	- Validate hexadecimal color codes with a maximum of 9 characters (one hash # plus up to 8 digits).
---

### 18. HTTP Methods

- Method Change:
	- Attempt to use incorrect HTTP methods (e.g., PUT/DELETE on a GET-only endpoint) and expect a 405 Method Not Allowed response.
---

### 19. Contract Verification

- Data Contracts:
	- Mandatory vs. Optional Fields:
		- Clearly document which fields are mandatory and which are optional.
		- Example:
			- Mandatory: userId, email, password
			- Optional: middleName, nickname, secondaryPhone
	- Schema Verification:
		- Validate that the JSON/XML response adheres to the defined schema, including required fields and data types.
- Request and Response:
	- Send all allowed properties with values and verify that the response contains the expected data.
	- Confirm that the returned JSON/XML is correctly formatted with all expected properties and values.
---

### 20. Error Messages

- Clarity and Consistency:
	- Ensure error messages are clear, descriptive, and provide actionable guidance.
	- Validate that similar error scenarios produce consistent messages across the API.
---

### 21. Headers

- Request Headers:
	- Verify that all required headers (e.g., Content-Type, Accept, Authorization) are present and correctly formatted.
	- Check for expected headers such as Cache-Control, X-Correlation-ID, or any custom headers defined in the contract.
---

### 22. Rate Limiting & Throttling

- Excessive Requests:
	- Confirm that the API returns a 429 Too Many Requests status when hit with excessive requests.
	- Verify that any provided rate limit headers correctly indicate the remaining quota and reset time.
---

### 23. Idempotency

- Consistent Results:
	- For safe and repeatable operations (e.g., GET, PUT, DELETE), ensure that repeated requests produce consistent results.
	- Validate that endpoints marked as idempotent in the contract behave as expected when the same request is sent multiple times.
---

### 24. CORS (Cross-Origin Resource Sharing)

- CORS Headers:
	- Verify that the API returns the proper CORS headers (e.g., Access-Control-Allow-Origin) when accessed from different origins.
	- Test with various origins to ensure cross-domain requests are handled according to the specification.
---

### 25. Addresses
- **Valid address**: `{"address":"1600 Amphitheatre Parkway, Mountain View, CA"} -H "Content-Type: application/json"` → expect 200 OK and parsed address object in response
- **Non-existent address**: `{"address":"1234 ThisStreet DoesNotExist, ZZ"} -H "Content-Type: application/json"` → expect 422 Unprocessable Entity with error “Address not found”
- **Missing “address” field**: `{}` -H "Content-Type: application/json" → expect 400 Bad Request and validation error mentioning “address is required”
- **Empty address string**: `{"address":""} -H "Content-Type: application/json"` → expect 400 Bad Request and “Address cannot be empty”
- **Whitespace-only address**: `{"address":"    "} -H "Content-Type: application/json"` → expect 400 Bad Request and “Address cannot be blank”
- **Overly long address (>255 chars)**: `{"address":"<256-char string>"} -H "Content-Type: application/json"` → expect 413 Payload Too Large or 400 Bad Request with “Address too long”
- **Malformed JSON**: `{"address":"123 Main St"` -H "Content-Type: application/json"\` → expect 400 Bad Request and “Malformed JSON”
- **Invalid field type (number instead of string)**: `{"address":12345} -H "Content-Type: application/json"` → expect 400 Bad Request and “Address must be a string”
- **SQL‐injection payload in address**: `{"address":"123 Main St; DROP TABLE users;"} -H "Content-Type: application/json"` → expect 400 Bad Request or input sanitized and rejected
- **Address with special characters**: `{"address":"45B Baker Street, Apt #2A"} -H "Content-Type: application/json"` → expect 200 OK and correctly parsed address
- **International/multilingual address**: `{"address":"улица Ленина, 10, Москва, Россия"} -H "Content-Type: application/json"` → expect 200 OK and localized fields returned
- **Partial address (missing city or zip)**: `{"address":"742 Evergreen Terrace"} -H "Content-Type: application/json"` → expect 422 Unprocessable Entity and “Incomplete address”
- **GET lookup of existing address**: `GET /api/addresses?address=221B%20Baker%20St -H "Accept: application/json"` → expect 200 OK with matching address details
- **GET lookup of non-existent address**: `GET /api/addresses?address=NoSuchPlace%20123 -H "Accept: application/json"` → expect 404 Not Found and error “Address not found”
---

### Additional Resources

- [Standard HTTP/HTTPS Response Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)
- Country-Specific Data:
	- When validating addresses, consider local postal code formats (e.g., UK postal codes or Chinese regional codes) and other country-specific address components.
- Data Contracts:
	- Ensure data contracts include detailed definitions of each field, indicating which are mandatory and which are optional. Use JSON Schema or similar tools for robust contract validation.
---
