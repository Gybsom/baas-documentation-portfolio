# Guides

This section provides practical guides to help you implement key features using our API.

---

### Paying a Boleto

A "boleto" is a popular Brazilian payment method. This guide will walk you through the process of enabling your users to pay a boleto using their account balance. The process involves three main steps: validating the boleto data, confirming the payment, and checking the final status.

**Step 1: Validate the Boleto Information**

Before processing a payment, it's crucial to validate the boleto's details, such as the amount and expiration date. You can do this by sending the payment slip's digitable line to our validation endpoint.

**API Call:**
First, make a `POST` request to the `/boletos/validate` endpoint.

```json
POST /boletos/validate
{
  "digitable_line": "23793.38128 60073.223304 33006.033331 8 98760000123456"
}
```

The API will respond with the boleto's details, including the amount, beneficiary, and due date. This allows you to display the information to your user for confirmation.

**Step 2: Initiate the Payment**

Once the user confirms the details, you can initiate the payment. This is done by sending a `POST` request to the `/boletos/pay` endpoint, including the digitable line and the amount.

**API Call:**

```json
POST /boletos/pay
{
  "digitable_line": "23793.38128 60073.223304 33006.033331 8 98760000123456",
  "amount": 1234.56,
  "payment_date": "2025-09-29"
}
```

The API will respond with a `unique transaction_id` and a `status` of processing.

**Step 3: Check the Payment Status**

Since boleto processing can take some time, you should periodically check the payment status.

API Call:
Make a `GET` request to `/boletos/{transaction_id}`.

```bash
GET /boletos/a1b2c3d4-e5f6-7890-g1h2-i3j4k5l6m7n8
```

The response will show the final status, which can be `completed` or `failed`. We recommend implementing webhooks to receive real-time status updates.

---

### Making a Pix Transfer

Pix is Brazil's instant payment system. This guide shows how to implement a Pix transfer from a user's account to a recipient's Pix key.

**Step 1: Get User Confirmation**

Your application should first collect the recipient's Pix key (it can be an email, phone number, or a random key) and the amount to be transferred. Display these details to the user for confirmation before proceeding.

**Step 2: Initiate the Pix Transfer**

With the user's confirmation, send the details to our Pix transfer endpoint.

**API Call:**

Make a `POST` request to `/pix/transfers`.

```json
POST /pix/transfers
{
  "amount": 150.00,
  "recipient": {
    "key_type": "email",
    "key_value": "receiver@example.com"
  },
  "description": "Payment for services"
}
```

The system will immediately attempt to process the transfer. The API response will include a `transaction_id` and the current `status`. For Pix, the status is often `completed` within seconds.

**Step 3: Verify the Transfer Status**

Although Pix transfers are fast, it is good practice to confirm the final status.

**API Call:**

Make a `GET` request to `/pix/transfers/{transaction_id}`.

```bash
GET /pix/transfers/z9y8x7w6-v5u4-3210-t9s8-r7q6p5o4n3m2
```

The response will confirm the final status, such as `completed` or `failed`. If the transfer fails, the response will include a `reason` field explaining the cause.