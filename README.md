### Ma3ahed Blog System API Documentation

#### Overview:

This API allows for managing a blog system, enabling operations on posts, comments, users, and categories.

#### Base URL:

`https://m3afed.e3lanotopia.software`

#### Authentication:

Most endpoints require authentication. Use Bearer token to authenticate requests.

---

### Endpoints:

#### 1. User Management

- **Create User**

  - **POST** `/users`
  - **Body**:
    ```json
    {
      "username": "string",
      "email": "string",
      "password": "string"
    }
    ```
  - **Response**: `201 Created`
    ```json
    {
      "id": "integer",
      "username": "string",
      "email": "string"
    }
    ```

- **Login User**
  - **POST** `/users/login`
  - **Body**:
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  - **Response**: `200 OK`
    ```json
    {
      "token": "string"
    }
    ```

#### 2. Post Management

- **Create Post**

  - **POST** `/posts`
  - **Authorization**: Bearer Token
  - **Body**:
    ```json
    {
      "title": "string",
      "content": "string",
      "category_id": "integer"
    }
    ```
  - **Response**: `201 Created`
    ```json
    {
      "id": "integer",
      "title": "string",
      "content": "string",
      "category_id": "integer",
      "created_at": "datetime"
    }
    ```

- **Get All Posts**
  - **GET** `/posts`
  - **Query Parameters**:
    - `page`: integer
    - `limit`: integer
  - **Response**: `200 OK`
    ```json
    [
      {
        "id": "integer",
        "title": "string",
        "content": "string",
        "category_name": "string",
        "created_at": "datetime"
      }
    ]
    ```

#### 3. Comment Management

- **Add Comment**
  - **POST** `/comments`
  - **Authorization**: Bearer Token
  - **Body**:
    ```json
    {
      "post_id": "integer",
      "content": "string"
    }
    ```
  - **Response**: `201 Created`
    ```json
    {
      "id": "integer",
      "post_id": "integer",
      "content": "string",
      "created_at": "datetime"
    }
    ```

#### 4. Category Management

- **Create Category**
  - **POST** `/categories`
  - **Authorization**: Bearer Token
  - **Body**:
    ```json
    {
      "name": "string"
    }
    ```
  - **Response**: `201 Created`
    ```json
    {
      "id": "integer",
      "name": "string"
    }
    ```

#### 5. Update User Profile

- **PUT** `/users/{userId}`
  - **Authorization**: Bearer Token
  - **Path Parameters**:
    - `userId`: integer
  - **Body**:
    ```json
    {
      "username": "string",
      "email": "string",
      "bio": "string"
    }
    ```
  - **Response**: `200 OK`
    ```json
    {
      "id": "integer",
      "username": "string",
      "email": "string",
      "bio": "string"
    }
    ```

#### 6. Delete User

- **DELETE** `/users/{userId}`
  - **Authorization**: Bearer Token
  - **Path Parameters**:
    - `userId`: integer
  - **Response**: `204 No Content`

#### 7. Update Post

- **PUT** `/posts/{postId}`
  - **Authorization**: Bearer Token
  - **Path Parameters**:
    - `postId`: integer
  - **Body**:
    ```json
    {
      "title": "string",
      "content": "string",
      "category_id": "integer"
    }
    ```
  - **Response**: `200 OK`
    ```json
    {
      "id": "integer",
      "title": "string",
      "content": "string",
      "category_id": "integer",
      "updated_at": "datetime"
    }
    ```

#### 8. Delete Post

- **DELETE** `/posts/{postId}`
  - **Authorization**: Bearer Token
  - **Path Parameters**:
    - `postId`: integer
  - **Response**: `204 No Content`

#### 9. Get User Posts

- **GET** `/users/{userId}/posts`
  - **Path Parameters**:
    - `userId`: integer
  - **Response**: `200 OK`
    ```json
    [
      {
        "id": "integer",
        "title": "string",
        "content": "string",
        "created_at": "datetime"
      }
    ]
    ```

#### 10. Tag Management

- **Create Tag**

  - **POST** `/tags`
  - **Authorization**: Bearer Token
  - **Body**:
    ```json
    {
      "name": "string"
    }
    ```
  - **Response**: `201 Created`
    ```json
    {
      "id": "integer",
      "name": "string"
    }
    ```

- **Get All Tags**

  - **GET** `/tags`
  - **Response**: `200 OK`
    ```json
    [
      {
        "id": "integer",
        "name": "string"
      }
    ]
    ```

- **Delete Tag**
  - **DELETE** `/tags/{tagId}`
  - **Authorization**: Bearer Token
  - **Path Parameters**:
    - `tagId`: integer
  - **Response**: `204 No Content`

#### 11. Search Posts by Tag

- **GET** `/tags/{tagId}/posts`
  - **Path Parameters**:
    - `tagId`: integer
  - **Response**: `200 OK`
    ```json
    [
      {
        "id": "integer",
        "title": "string",
        "content": "string",
        "created_at": "datetime"
      }
    ]
    ```

### Notes:

1. **Status Codes**: Each endpoint includes typical HTTP status codes that may be returned (e.g., `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`).
2. **Error Handling**: Include a standardized error payload for errors.
3. **Pagination**: For endpoints that return multiple items, support pagination.
4. **Security**: Include security considerations such as SSL, input sanitation, etc.
