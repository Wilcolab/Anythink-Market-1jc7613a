# Anythink Market Backend

The Anythink Market backend is Node web app written with [Express](https://expressjs.com/)

## Dependencies

- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) - For generating JWTs used by authentication
- [mongoose](https://github.com/Automattic/mongoose) - For modeling and mapping MongoDB data to javascript
- [mongoose-unique-validator](https://github.com/blakehaswell/mongoose-unique-validator) - For handling unique validation errors in Mongoose. Mongoose only handles validation at the document level, so a unique index across a collection will throw an exception at the driver level. The `mongoose-unique-validator` plugin helps us by formatting the error like a normal mongoose `ValidationError`.
- [passport](https://github.com/jaredhanson/passport) - For handling user authentication
- [slug](https://github.com/dodo/node-slug) - For encoding titles into a URL-friendly format

## Application Structure

- `app.js` - The entry point to our application. This file defines our express server and connects it to MongoDB using mongoose. It also requires the routes and models we'll be using in the application.
- `config/` - This folder contains configuration for passport as well as a central location for configuration/environment variables.
- `routes/` - This folder contains the route definitions for our API.
- `models/` - This folder contains the schema definitions for our Mongoose models.

## Error Handling

In `routes/api/index.js`, we define a error-handling middleware for handling Mongoose's `ValidationError`. This middleware will respond with a 422 status code and format the response to have [error messages the clients can understand](https://github.com/gothinkster/realworld/blob/master/API.md#errors-and-status-codes)

## Comments API

### DELETE `/api/comments/:id`

Deletes a comment by its unique identifier.

**Request Parameters:**

- `id` (string, required): The unique identifier of the comment to be deleted.

**Responses:**

- `200 OK`: `{ "message": "Comment deleted successfully" }` — Comment was found and deleted.
- `404 Not Found`: `{ "message": "Comment not found" }` — No comment with the specified ID exists.
- `500 Internal Server Error`: `{ "message": "Internal server error" }` — Error occurred during deletion.

**Example Request:**

```
DELETE /api/comments/60d21b4667d0d8992e610c85
```

**Example Success Response:**

```json
{
  "message": "Comment deleted successfully"
}
```

**Example Error Response (Not Found):**

```json
{
  "message": "Comment not found"
}
```
