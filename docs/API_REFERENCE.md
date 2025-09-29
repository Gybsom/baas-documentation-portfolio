# API Reference

This section contains detailed information about our available endpoints, including headers, request parameters, and possible responses. All API requests require an `Authorization` header and should have a `Content-Type` of `application/json`.

---

## **Boletos**

Endpoints related to validating and paying boletos.

### `POST /boletos/validate`

Validates a boleto's digitable line to retrieve its details without processing a payment. This is useful for displaying confirmation information to the end-user before they commit to the payment.

**Headers**

| Header          | Type   | Description                                           |
|-----------------|--------|-------------------------------------------------------|
| `Authorization` | String | Your API authentication token. Ex: `Bearer your_token` |
| `Content-Type`  | String | Must be `application/json`.                           |

**Request Body**

| Field          | Type   | Description                                              | Required |
|----------------|--------|----------------------------------------------------------|----------|
| `digitable_line` | String | The numerical, digitable line of the boleto to be validated. | Yes      |

**Responses**

| Status Code | Reason                 | Description                                                                                             |
|-------------|------------------------|---------------------------------------------------------------------------------------------------------|
| `200 OK`      | Success                | The digitable line is valid and its data was successfully retrieved.                                    |
| `400 Bad Request` | Invalid Format         | The provided `digitable_line` has an invalid format (e.g., wrong length, non-numeric characters).     |
| `422 Unprocessable Entity` | Invalid Boleto         | The digitable line is well-formatted but corresponds to an invalid or expired boleto.          |

**Example: Successful Response (`200 OK`)**
```json
{
  "valid": true,
  "amount": 1234.56,
  "due_date": "2025-10-10",
  "beneficiary": {
    "name": "Example Company Inc.",
    "document": "12.345.678/0001-99"
  },
  "recipient": "Example Recipient Name"
}
```

**Example: Error Response (`400 Bad Request`)**
```json
{
  "error": "Bad Request",
  "message": "Field 'digitable_line' must contain only numbers and have a valid length."
}
```
