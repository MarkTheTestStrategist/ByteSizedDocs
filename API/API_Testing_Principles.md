# API Testing Principles

## Overview
This document outlines the fundamental principles we follow when testing APIs, applicable to any company.

## Tools
- Postman is the primary tool for API testing.
- Logging: To be determined
- Automation: To be determined
- Newman or Playwright

## The Principles
These principles serve as guidelines to ensure comprehensive API testing while offering best practices for structuring collections.

## Data
- The allowed minimum and maximum values should align with the database constraints.
- If not specified, the maximum length for varchar fields in the database is 8,000 characters.
- Each property should strictly enforce its designated data type.
  - **Example:** A boolean field should not accept varchar values.

## Mandatory Properties
- A request should successfully execute using only the mandatory properties set to their minimum or maximum values.
- User-friendly validation should prevent requests from being sent without all mandatory fields and valid minimum/maximum values.

### Validation
- All validation messages should be user-friendly.
  - **Example:** If the "name" property is missing, the 400 Bad Request response should return an error message stating that "name" is required.
- For customer-facing APIs, validation messages should remain user-friendly but less detailed to avoid exposing information that could be exploited by attackers.

## Authorization
- All requests requiring an API key or JWT must return a **401 Unauthorized** response if the credential is missing or invalid.
- All other valid requests should return a **200 OK** (successful response) or **201 Created** (when a new resource is generated).

## Environments
- We should avoid relying on stored environment or global variables for values such as base URLs or API keys, as they may persist across test runs and obscure potential bugs.
- Test environments should be cleared before each test session to ensure consistency and prevent data contamination.
- Base URLs, API keys, and similar configurations should be stored within the main folder of the collection, ensuring a single source of truth for all subfolders.

## Setup Script
- Using a setup script ensures a single source of truth, reducing duplication and simplifying maintenance.
- The setup script should begin by clearing environments using:
  ```javascript
  pm.environment.clear();
  pm.global.clear();
  ```
- It can then set up variables in advance of running requests. These variables can include dynamically generated values, such as unique usernames, email addresses, or country-specific test data.
- Authentication can be acquired upfront, eliminating the need to repeatedly execute the "login" request.

## Test Coverage
To ensure comprehensive API testing, the following aspects should be covered:
- **Response Time Performance**: Ensure APIs meet performance benchmarks.
- **Edge Case Scenarios**: Test large payloads, invalid formats, and unexpected inputs.
- **Security Vulnerabilities**: Validate against SQL injection, cross-site scripting (XSS), and unauthorized access attempts.

## Error Handling
Expected behaviors for common API errors:
- **400 Bad Request**: Invalid input
- **401 Unauthorized**: Missing or invalid authentication
- **403 Forbidden**: Insufficient permissions
- **404 Not Found**: Nonexistent resource
- **500 Internal Server Error**: Unexpected failures

