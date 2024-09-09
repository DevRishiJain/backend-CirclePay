# Intergalactic Trade Network API

## Trades

### POST /api/trades
Create a new trade transaction.

Request body:
```json
{
  "sellerStationId": "string",
  "buyerStationId": "string",
  "items": [
    {
      "itemId": "string",
      "quantity": "number",
      "price": "number"
    }
  ]
}
```

Response:
```json
{
  "transactionId": "string",
  "status": "string",
  "totalAmount": "number"
}
```

### GET /api/trades/{transactionId}
Retrieve details of a trade transaction.

Response:
```json
{
  "transactionId": "string",
  "sellerStationId": "string",
  "buyerStationId": "string",
  "items": [
    {
      "itemId": "string",
      "quantity": "number",
      "price": "number"
    }
  ],
  "status": "string",
  "totalAmount": "number",
  "timestamp": "string"
}
```

## Cargo

### POST /api/cargo
Create a new cargo shipment.

Request body:
```json
{
  "originStationId": "string",
  "destinationStationId": "string",
  "items": [
    {
      "itemId": "string",
      "quantity": "number"
    }
  ],
  "estimatedArrival": "string"
}
```

Response:
```json
{
  "shipmentId": "string",
  "status": "string"
}
```

### GET /api/cargo/{shipmentId}
Retrieve cargo shipment details.

Response:
```json
{
  "shipmentId": "string",
  "originStationId": "string",
  "destinationStationId": "string",
  "items": [
    {
      "itemId": "string",
      "quantity": "number"
    }
  ],
  "status": "string",
  "estimatedArrival": "string",
  "currentLocation": "string"
}
```

## Inventory

### GET /api/inventory/{stationId}
Retrieve inventory levels for a space station.

Response:
```json
{
  "stationId": "string",
  "inventory": [
    {
      "itemId": "string",
      "quantity": "number"
    }
  ]
}
```

## Real-time Updates

### GET /api/updates/real-time
Retrieve real-time updates on trade and cargo status.

Response (Server-Sent Events):
```
event: trade_update
data: {"transactionId": "string", "status": "string"}

event: cargo_update
data: {"shipmentId": "string", "status": "string", "currentLocation": "string"}

event: inventory_update
data: {"stationId": "string", "itemId": "string", "newQuantity": "number"}
```

Error Handling:
- 200 OK: Successful request
- 400 Bad Request: Invalid input
- 401 Unauthorized: Authentication failed
- 404 Not Found: Resource not found
- 500 Internal Server Error: Server-side error

All endpoints require authentication via JWT token in the Authorization header.
