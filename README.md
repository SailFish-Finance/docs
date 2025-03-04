# API Documentation

This provides an overview for adding Liquidity and Token to SailFish.

## Base URL

All API requests are made to the following base URL: `https://app.sailfish.finance`. The API uses IP whitelisting for authentication and supports operations for creating and retrieving tokens and other operations.

## Authentication

No authentication credentials are required. The IP (domain) from which the request are sent needs to be whitelisted by the SailFish team. Please contact support `engineering@sailfish.finance`

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

- `Content-Type`: `multipart/form-data`

**Body:**

```json
{
  "name": "Token Name",
  "address": "0xAddress",
  "logo": "file", // The logo file is handled as multipart/form-data
  "created_at": "2024-08-19T12:34:56.789Z"
  "dapp": "<dapp-name>" // optional. used for categorizing whitelisted pools
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

## Adding Liquidity

### Initializing Liquidity Pool and Setting Pool Ratio - V3 (And Adding Initial Liquidity)

**URL**: Pool Wizard <https://app.sailfish.finance/pool/wizard>

#### **Steps to initial pool**

- **Select Pool Version**: Select the V3 Pool.
- **Select Tokens (Pool pair)**: Choose the tokens you want to initialize a pool for.
- **Set Initial Pool Ratio**: Set your pool ratio. 1 of Token A equals to `x` of TOKEN B.
- **Set a Fee Tier**: Choose the fee tier that works best for the pool pair.
- **Confirm Pool Ratio**
- **Create and Initialize Pool with ratio**

### Adding Liquidity to Newly Created Pool - V3

**URL**: Pool Wizard <https://app.sailfish.finance/pool/wizard>

#### **Steps to adding initial liquidity**

- **Select Pool Version**: Select the V3 Pool.
- **Select Tokens (Pool pair)**: Choose the tokens you want to add initial liquidity for.
- **Select the Fee Tier**: Choose the fee tier for the pool pair.
- **Then Deposit**: If pool exist, a button with the text: "Already exists: Go to Deposit" should be visible.

### Adding Liquidity to Existing Created Pool - V3

**URL**: Liquidity <https://app.sailfish.finance/pool/liquidity>

#### **Steps to adding liquidity**

- **Select Pool**: Choose a pool from the list of pools.
- **Set Price Range**: Choose a price range(Narrow, Common, Wide, Full).
- **Supply Amount**
- **Add Liquidity(Create Position)**: Create a Position by adding Liquidity.

### Increasing/Decreasing Liquidity for a specific position - V3

**URL**: Portfolio <https://app.sailfish.finance/portfolio>

#### **Steps to increasing/decreasing liquidity**

- **Select Position**: Choose a position from the list of positions.
- **Choose Remove or Add Liquidity**
- **Enter Amount**: Percentage to remove or add.

If you have any questions or need further assistance, please contact support: `engineering@sailfish.finance`.

This `Readme.md` file provides comprehensive documentation for using the API for generating Token, managing tokens, and adding Liquidity. It includes examples of requests and responses for each operation.
