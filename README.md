# API Documentation

This provides an overview for adding Liquidity and Token to SailFish.

## Base URL

All API requests are made to the following base URL: `https://app.sailfish.finance`. The API uses IP whitelisting for authentication and supports operations for creating and retrieving tokens and other operations.

## Authentication

No authentication credentials are required. The IP (domain) from which the request is sent needs to be whitelisted by the SailFish team. Please contact support `engineering@sailfish.finance`

## Endpoints

### Tokens API

#### Get Tokens

**Endpoint:** `/api/tokens`

**Method:** GET

**Description:** Retrieves a list of all tokens.

**Request Example:**

```javascript
const fetchTokens = async () => {
  const response = await fetch("https://app.sailfish.finance/api/tokens");

  if (!response.ok) {
    const error = await response.json();
    console.error("Error:", error.message);
    return;
  }

  const data = await response.json();
  console.log("Tokens:", data.tokens);
};

fetchTokens();
```

**Response Example:**

```json
{
  "tokens": [
    {
      "_id": "id",
      "name": "Token Name",
      "address": "0xAddress",
      "logo_url": "https://example.com/logo.png",
      "created_at": "2024-08-19T12:34:56.789Z"
    }
  ]
}
```

#### Create Token

**Endpoint:** `/api/tokens`

**Method:** POST

**Headers:**

- `Content-Type`: `application/json`

**Body:**

```json
{
  "name": "Token Name",
  "address": "0xAddress",
  "logo": "file", // The logo file is handled as multipart/form-data
  "created_at": "2024-08-19T12:34:56.789Z"
}
```

**Request Example:**

```javascript
const formData = new FormData();
formData.append("name", "Token Name");
formData.append("address", "0xAddress");
formData.append("created_at", new Date().toISOString());
formData.append("logo", fileInput.files[0]); // Assuming you have a file input

const response = await fetch("https://app.sailfish.finance/api/tokens", {
  method: "POST",
  body: formData,
});
```

**Response Example:**

```json
{
  "message": "Token created successfully",
  "token": {
    "_id": "id",
    "name": "Token Name",
    "address": "0xAddress",
    "logo_url": "https://example.com/logo.png",
    "created_at": "2024-08-19T12:34:56.789Z"
  }
}
```

## Error Handling

- **401 Unauthorized**: API key is missing or invalid.
- **400 Bad Request**: Missing required fields or invalid data.
- **409 Conflict**: Duplicate `pair_address` or invalid token IDs.
- **500 Internal Server Error**: Unexpected server issues.

If you have any questions or need further assistance, please contact support: `support@sailfish.finance`.

This `Readme.md` file provides comprehensive documentation for using the API for generating Token, managing tokens, and adding Liquidity. It includes examples of requests and responses for each operation.
