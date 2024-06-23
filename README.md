
# Blog API Application

## Tech Stack

- Server - TypeScript, Node, Express, MongoDB, Mongoose, JWT, Cloudinary
- Automated API Testing - Postman

# API Features

- Authentication & Authorization
- User CRUD operations
- Category CRUD operations
- Post CRUD operations
- Comment CRUD operations
- Profile photo upload
- System blocking user if inactive for 30 days
- Admin can block a user
- Admin can unblock a blocked user
- A user can block different users
- A user who block another user cannot see his/her posts
- Last date a post was created
- Check if a user is active or not
- Check last date a user was active
- Changing user award base on number of posts created by the user
- A user can follow and unfollow another user
- Get following and followers count
- Get total profile viewers count
- Get posts created count
- Get blocked counts
- Get all users who views someone's profile

# ENDPOINTS

- [API Authentication](#api-authentication)

  - [User Registration](#user-registration)
  - [User Login](#user-login)

- [Users](#user-api-reference)

  - [Get User Profile](#get-user-profile)
  - [Get All Users](#get-all-users)
  - [Upload Profile Photo](#upload-profile-photo)
  - [Update User Profile](#update-user-profile)
  - [Update User Password](#update-user-password)
  - [View a User Profile](#view-a-user-profile)
  - [Following a User](#following-a-user)
  - [UnFollowing a User](#unfollowing-a-user)
  - [Block Another User](#block-user)
  - [Unblock Another User](#unblock-user)
  - [Admin Blocking a User](#admin-blocking-a-user)
  - [Admin Unblocking a User](#admin-unblocking-a-user)
  - [Delete Your Account](#delete-your-account)

- [Categories](#categories-api-reference)

  - [Create Category](#create-category)
  - [Get All Categories](#get-all-categories)
  - [Get Single Category](#get-single-category)
  - [Update Category](#update-category)
  - [Delete Category](#delete-category)

- [Posts](#posts-api-reference)

  - [Create Post](#create-post)
  - [Get All Posts](#get-all-posts)
  - [Get Single Post](#get-single-post)
  - [Update Post](#update-post)
  - [Toggle Post Like](#toggle-post-like)
  - [Toggle Post Dislike](#toggle-post-dislike)
  - [Delete Post](#delete-post)

- [Comments](#comment-api-reference)

  - [Create Comment](#create-comment)
  - [Get All Comments](#get-all-comments)
  - [Get Single Comment](#get-single-comment)
  - [Update Comment](#update-comment)
  - [Delete Comment](#delete-comment)

## Run Locally

Clone the project

```bash
  git clone https://link-to-project
```

Go to the project directory

```bash
  cd node-blog
```

Install dependencies

```bash
  npm install
```

Start the server

```bash
  npm run dev
```

## Environment Variables

To run this project, you will need to add the following environment variables to your .env file

`MONGO_URI`
`JWT_SECRET`
`CLOUDINARY_CLOUD_NAME`
`CLOUDINARY_API_KEY`
`CLOUDINARY_API_SECRET`

# API Authentication

All endpoints except register & login, require authentication. For example, to get/create/update/delete a post, you need to register/login by your API client and obtain an access token.

The endpoints that require authentication expect a bearer token sent in the `Authorization` header.

**Example**:

`Authorization: Bearer YOUR_TOKEN`

The request body needs to be in JSON format.

# **User API Reference**

## **User Registration**

```http
POST /api/v1/users/register
```

| Parameter        | Type     | Description     | Required |
| :--------------- | :------- | :-------------- | :------- |
| `firstName`      | `string` | Your first name | yes      |
| `lastName`       | `string` | Your last name  | yes      |
| `email`          | `string` | Your email      | yes      |
| `password`       | `string` | Your password   | yes      |

Example request body:

```javascript
{
  "firstName":"your first name",
  "lastName":"your last name",
  "email":"your email"
  "password":"your password"
}
```

## **User Login**

```http
POST /api/v1/users/login
```

| Parameter        | Type     | Description   | Required |
| :--------------- | :------- | :------------ | :------- |
| `email`          | `string` | Your email    | yes      |
| `password`       | `string` | Your password | yes      |

Example request body:

```javascript
{
  "email":"your email"
  "password":"your password"
}
```

## **Get user profile**

```http
GET /api/v1/users/profile
```

| Parameter        | Type     | Description | Required |
| :--------------- | :------- | :---------- | :------- |
| `authentication` | `string` | Your token  | yes      |

## **Get all users**

```http
GET /api/v1/users
```

| Parameter        | Type     | Description | Required |
| :--------------- | :------- | :---------- | :------- |
| `authentication` | `string` | Your token  | yes      |

## **Upload Profile Photo**

```http
POST /api/v1/users/profile-photo-upload
```

| Parameter        | Type     | Description     | Required |
| :--------------- | :------- | :-------------- | :------- |
| `authentication` | `string` | Your token      | yes      |
| `profilePhoto`   | `string` | Image to upload | yes      |

## **Update user profile**

```http
PUT /api/v1/users/:id
```

| Parameter        | Type     | Description           | Required |
| :--------------- | :------- | :-------------------- | :------- |
| `authentication` | `string` | Your token            | yes      |
| `email`          | `string` | Enter your email      | no       |
| `firstName`      | `string` | Enter your first name | no       |
| `lastName`       | `string` | Enter your last name  | no       |

Example request body:

```javascript
{
  "email":"value",
  "firstName":"value",
  "lastName":"value",
}
```

## **Update user password**

```http
PUT /api/v1/users/update-password
```

| Parameter           | Type     | Description                   | Required |
| :------------------ | :------- | :---------------------------- | :------- |
| `authentication`    | `string` | Your token                    | yes      |
| `oldPassword`       | `string` | Enter your old password       | yes      |
| `newPassword`       | `string` | Enter your new password       | yes      |
| `confirmPassword`   | `string` | Enter your new password again | yes      |

Example request body:

```javascript
{
  "oldPassword":"value",
  "newPassword":"value",
  "confirmPassword":"value"
}
```

## **View a user profile**

```http
GET /api/v1/users/profile-viewers/:id
```

| Parameter        | Type     | Description                                 | Required |
| :--------------- | :------- | :------------------------------------------ | :------- |
| `authentication` | `string` | Your token                                  | yes      |
| `id`             | `string` | ID of the user you want to view his profile | yes      |

## **Following a user**

```http
GET /api/v1/users/follow/:id
```

| Parameter        | Type     | Description                       | Required |
| :--------------- | :------- | :-------------------------------- | :------- |
| `authentication` | `string` | Your token                        | yes      |
| `id`             | `string` | ID of the user you want to follow | yes      |

## **UnFollowing a user**

```http
GET /api/v1/users/unfollow/:id
```

| Parameter        | Type     | Description                       | Required |
| :--------------- | :------- | :-------------------------------- | :------- |
| `authentication` | `string` | Your token                        | yes      |
| `id`             | `string` | ID of the user you want to follow | yes      |

## **Block user**

```http
GET /api/v1/users/block/:id
```

| Parameter        | Type     | Description                      | Required |
| :--------------- | :------- | :------------------------------- | :------- |
| `authentication` | `string` | Your token                       | yes      |
| `id`             | `string` | Id of the user you want to block | yes      |

## **Unblock user**

```http
GET /api/v1/users/unblock/:id
```

| Parameter        | Type     | Description                        | Required |
| :--------------- | :------- | :--------------------------------- | :------- |
| `authentication` | `string` | Your token                         | yes      |
| `id`             | `string` | Id of the user you want to unblock | yes      |

## **Admin blocking a user**

```http
GET /api/v1/users/admin-block/:id
```

| Parameter        | Type     | Description                      | Required |
| :--------------- | :------- | :------------------------------- | :------- |
| `authentication` | `string` | Your token                       | yes      |
| `id`             | `string` | Id of the user you want to block | yes      |

## **Admin unblocking a user**

```http
GET /api/v1/users/admin-unblock/:id
```

| Parameter        | Type     | Description                        | Required |
| :--------------- | :------- | :--------------------------------- | :------- |
| `authentication` | `string` | Your token                         | yes      |
| `id`             | `string` | Id of the user you want to unblock | yes      |

## **Delete your account**

```http
DELETE /api/v1/users/delete-account
```

| Parameter        | Type     | Description | Required |
| :--------------- | :------- | :---------- | :------- |
| `authentication` | `string` | Your token  | yes      |

# **Categories API Reference**

## **Create Category**

```http
POST /api/v1/categories
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `title`          | `string` | Category title | yes      |

Example request body:

```javascript
{
  "title":"value",
}
```

## **Get All Categories**

```http
GET /api/v1/categories
```

| Parameter        | Type     | Description        | Required |
| :--------------- | :------- | :----------------- | :------- |
| `authentication` | `string` | Your token         | yes      |

## **Get Single Category**

```http
GET /api/v1/categories/:id
```

| Parameter        | Type     | Description        | Required |
| :--------------- | :------- | :----------------- | :------- |
| `authentication` | `string` | Your token         | yes      |
| `id`             | `string` | ID of the category | yes      |

## **Update Category**

```http
PUT /api/v1/categories/:id
```

| Parameter        | Type     | Description        | Required |
| :--------------- | :------- | :----------------- | :------- |
| `authentication` | `string` | Your token         | yes      |
| `id`             | `string` | ID of the category | yes      |
| `title`          | `string` | Category title     | yes      |

Example request body:

```javascript
{
  "title":"value",
}
```

## **Delete Category**

```http
DELETE /api/v1/categories/:id
```

| Parameter        | Type     | Description        | Required |
| :--------------- | :------- | :----------------- | :------- |
| `authentication` | `string` | Your token         | yes      |
| `id`             | `string` | ID of the category | yes      |

# **Posts API Reference**

## **Create Post**

```http
POST /api/v1/posts
```

| Parameter        | Type     | Description        | Required |
| :--------------- | :------- | :----------------- | :------- |
| `authentication` | `string` | Your token         | yes      |
| `title`          | `string` | Post title         | yes      |
| `description`    | `string` | Post description   | yes      |
| `category`       | `string` | ID of the category | yes      |
| `photo`          | `string` | Image of the post  | yes      |

Example request body:

```javascript
{
  "title":"value",
  "description":"value",
  "category":"value",
  "photo":"photo",
}
```

## **Get All Posts**

```http
GET /api/v1/posts
```

| Parameter        | Type     | Description | Required |
| :--------------- | :------- | :---------- | :------- |
| `authentication` | `string` | Your token  | yes      |

## **Get Single Post**

```http
GET /api/v1/posts/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

## **Update Post**

```http
PATCH /api/v1/posts/:id
```

| Parameter        | Type     | Description             | Required |
| :--------------- | :------- | :---------------------- | :------- |
| `authentication` | `string` | Your token              | yes      |
| `id`             | `string` | ID of the post          | yes      |
| `title`          | `string` | Title of the post       | no       |
| `description`    | `string` | Description of the post | no       |
| `category`       | `string` | Category of the post    | no       |
| `photo`          | `string` | Photo of the post       | no       |

Example request body:

```javascript
{
  "title":"value",
  "description":"value",
  "category":"value",
  "photo":"photo",
}
```

## **Toggle Post like**

```http
GET /api/v1/posts/likes/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

## **Toggle Post dislike**

```http
GET /api/v1/posts/dislikes/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

## **Delete Post**

```http
DELETE /api/v1/posts/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

# **Comment API Reference**

## **Create Comment**

```http
POST /api/v1/comments
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `content`        | `string` | Comment        | yes      |

Example request body:

```javascript
{
  "content":"value",
}
```

## **Get All Comments**

```http
GET /api/v1/comments
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |

## **Get Single Comment**

```http
GET /api/v1/comments/:id
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |
| `id`             | `string` | ID of the comment | yes      |

## **Update Comment**

```http
PUT /api/v1/comments/:id
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |
| `id`             | `string` | ID of the comment | yes      |
| `content`        | `string` | Comment           | yes      |

Example request body:

```javascript
{
  "content":"value",
}
```

## **Delete Comment**

```http
DELETE /api/v1/comments/:id
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |
| `id`             | `string` | ID of the comment | yes      |
