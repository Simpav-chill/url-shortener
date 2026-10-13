# Overview
## Description
The service generates a short unique alias for a long URL and redirects users from that alias back to the original URL. Also collects statistics of clicks: device, geolocation by ip, referrer, and transmit it to background analytics service. 
## Target audience
Regular users that are uncomfortable with long URLs.
# Architecture and technical stack
## Main stack

| Part             | Technology              | Version     |
| ---------------- | ----------------------- | ----------- |
| Language         | Java                    | 21          |
| Framework        | Spring Boot             | *add later* |
| Database         | PostgreSQL              | *add later* |
| API docs         | Swagger UI with OpenAPI | *add later* |
| Unit test        | JUnit + Mockito         | *add later* |
| Integration test | Testcontainers          | *add later* |
| Containerization | Docker compose          | *add later* |
## Schema
![[assets/url-shortener-architecture-schema.svg]]
# Features and REST API
## Main features
### MVP (current)
- shorten URLs
- redirect from a short URL to a long one 
### V.2
- cache the most frequently used data
- collect statistics
- use message brockers
## API endpoints
Root endpoint – /api/{versionNumber} (e.g. /api/v1)

| Path          | API method | Description                                                                    |
| ------------- | ---------- | ------------------------------------------------------------------------------ |
| /health       | GET        | Check service health                                                           |
| /link/shorten | POST       | Provide a long link to shorten it, the service returns back the shortened link |
| /{linkAlias}  | GET        | Provide a shortened link, the service redirects to a long link                 |
# Data model
## Entities and relationships
### Entities
#### shortened_url

| Key         | Attribute name | Description                           | Constraints                      |
| ----------- | -------------- | ------------------------------------- | -------------------------------- |
| Primary key | id             | Identifition attribute                | Unique, not null                 |
|             | short_url      | Stores shortened URL matched long one | Unique, 6 chars length, not null |
|             | long_url       | Stores original url (long one)        | Unique, not null                 |

### Relashionships
There's no relationships in MVP database.
## Migrations
This service uses Liquibase database migration tool. The cause of using this tool is that it's more convenient than Flyway in a comparison in various aspects. [Source with a comparison between these two tools](https://www.baeldung.com/liquibase-vs-flyway)
# Engineering practices
## Testing 
### Tools
Unit testing implements with JUnit and Mockito. Integration testing implements with Testcontainers.
### Testing matrix

| Requirement | Unit tests | Integration tests | Status |
| ----------- | ---------- | ----------------- | ------ |
|             |            |                   |        |

## Security (delete if there's no any description for this sector)
## Exception handling
### Global exception handler
Exceptions are handled by GlobalHandlerException. 
### Standardized response format
RFC 7807 Problem Details is used as standardized error messagees structure. Example of a look of an HTTP response ([took from this site](https://www.mscharhag.com/api-design/rest-error-format)):
```
HTTP/1.1 400 Bad request
Content-Type: application/problem+json
Content-Language: en

{
    "type": "https://api.my-cool-example.com/problems/required-field-missing",
    "title": "Required field is missing",
    "detail": "Article with id 1234 cannot be updated because the required field 'title' is missing",
    "status": 400,
    "instance": "/articles/1234"
}
``` 
## Logging
The app uses SLF4J facade with Logback implementation. 
## Monitoring
Not implemented yet.
## API documentation 
*Describe how to open docs here.*
# Getting started (coming soon)
## Prerequisites
## Launch command
## Environment variables
