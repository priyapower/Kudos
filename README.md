# Kudos
CRUD project with Python BE and React FE

# User Stories
## Backend Stories
* As an authenticated user I want to favorite an github open source project
* As an authenticated user I want to unfavorite an github open source project
* As an authenticated user I want to list all bookmarked github open source projects I’ve previously favorited

## Backend RESTful endpoints
* A normal ReST API will expose endpoints so clients can create, update, delete, read and list all resources. By end of this section your back-end application will be capable to handle the following HTTP calls:
* C reate is commonly associated with the HTTP POST method (response status of 201)
* R ead is commonly associated with the HTTP GET method (response status of 200); Can be used to read a single object or retrieve all objects
* U pdate is commonly associated with the HTTP PUT || PATCH methods (response status of 200); PUT == updates the entire object; PATCH == updates partial object
* D elete is commonly associated with the HTTP DELETE method (response status of 204)
```python
# For the authenticated user, fetches all favorited github open source projects (READ ALL)
GET /kudos

# Favorite a github open source project for the authenticated user (CREATE)
POST /kudos

# Unfavorite a favorited github open source project (DELETE)
DELETE /kudos/:id
```
* _If time, add READ ONE, UPDATE WHOLE, and UPDATE PARTIAL_


