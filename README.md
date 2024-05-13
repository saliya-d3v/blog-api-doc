
# Blog API Application

## Tech Stack

__Server:__Node, Express, MongoDB, Mongoose, JWT, Cloudinary

# API Features

- Authentication & Authorization
- Post CRUD operations
- Comment functionality
- System blocking user if inactive for 30 days
- Admin can block a user
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
- Admin can unblock a blocked user
- Update password
- Profile photo uploaded
- A user can close his/her account

# ENDPOINTS

- [API Authentication](#api-authentication)

  - [User Registration](#user-registration)
  - [User Login](#user-login)

- [Users](#user-api-reference)

  - [Get my profile](#get-my-profile)
  - [Get all users](#get-all-users)
  - [View a user profile Count](#view-a-user-profile)
  - [Following a user](#following-a-user)
  - [UnFollowing-a-user](#unfollowing-a-user)
  - [Update user password](#update-user-password)
  - [Update your profile](#update-your-profile)
  - [Block another user](#block-user)
  - [Unblock another user](#unblock-user)
  - [Admin blocking a user](#admin-blocking-a-user)
  - [Admin Unblocking a user](#admin-unblocking-a-user)
  - [Delete your account](#delete-your-account)
  - [Upload Profile Photo](#upload-profile-photo)

- [Posts](#posts-api-reference)

  - [Create Post](#create-post)
  - [Get All Posts](#get-all-posts)
  - [Get Single Post](#get-single-post)
  - [Toggle Post like](#toggle-post-like)
  - [Toggle Post dislike](#toggle-post-dislike)
  - [Update Post](#update-post)
  - [Delete Post](#delete-post)

- [Comments](#comment-api-reference)
  - [Create comment](#create-comment)
  - [Get Single post](#get-single-comment)
  - [Update post](#update-comment)
  - [Delete post](#delete-comment)

# API Authentication

Some endpoints may require authentication. for example, To create/delete/update a post, you need to register by your API client and obtain an access token.

The endpoints that require authentication expect a bearer token sent in the `Authorization header`.

**Example**:

`Authorization: Bearer YOUR TOKEN`

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
| `authentication` | `string` | Your token    | no       |
| `email`          | `string` | Your email    | yes      |
| `password`       | `string` | Your password | yes      |

Example request body:

```javascript
{
  "email":"your email"
  "password":"your password"
}
```

## **Get my profile**

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
| `authentication` | `string` | Your token  | no       |

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

## **Update user password**

```http
PUT /api/v1/users/update-password
```

| Parameter        | Type     | Description         | Required |
| :--------------- | :------- | :------------------ | :------- |
| `authentication` | `string` | Your token          | yes      |
| `password`       | `string` | Enter your password | yes      |

Example request body:

```javascript
{
  "password":"value"
}
```

## **Update your profile**

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

## **Upload Profile Photo**

```http
POST /api/v1/users/profile-photo-upload
```

| Parameter        | Type     | Description     | Required |
| :--------------- | :------- | :-------------- | :------- |
| `authentication` | `string` | Your token      | yes      |
| `profilePhoto`   | `string` | Image to upload | yes      |

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
| `authentication` | `string` | Your token  | no       |

## **Get Single Post**

```http
GET /api/v1/posts/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

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

## **Update Post**

```http
PUT /api/v1/posts/:id
```

| Parameter        | Type     | Description             | Required |
| :--------------- | :------- | :---------------------- | :------- |
| `authentication` | `string` | Your token              | yes      |
| `id`             | `string` | ID of the post          | yes      |
| `title`          | `string` | title of the post       | yes      |
| `description`    | `string` | description of the post | yes      |
| `category`       | `string` | category of the post    | yes      |
| `photo`          | `string` | photo of the post       | yes      |

Example request body:

```javascript
{
  "title":"value",
  "description":"value",
  "category":"value",
  "photo":"photo",
}
```

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
POST /api/v1/comments/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |

## **Get Single Comment**

```http
GET /api/v1/comments/:id
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |
| `id`             | `string` | ID of the comment | yes      |

## **Delete Comment**

```http
DELETE /api/v1/comments/:id
```

| Parameter        | Type     | Description       | Required |
| :--------------- | :------- | :---------------- | :------- |
| `authentication` | `string` | Your token        | yes      |
| `id`             | `string` | ID of the comment | yes      |

## **Update Comment**

```http
PUT /api/v1/comments/:id
```

| Parameter        | Type     | Description    | Required |
| :--------------- | :------- | :------------- | :------- |
| `authentication` | `string` | Your token     | yes      |
| `id`             | `string` | ID of the post | yes      |
