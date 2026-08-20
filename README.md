Name: Rishi Thakker
Roll No: 150096725068
Cohort: Sam Altman


## Endpoints

### Auth

| Method | Endpoint | Auth | Input Body | Output |
|--------|----------|------|------------|--------|
| POST | `/register` | No | `{ "username": string, "email": string, "password": string }` | `201` → `{ message, user: { id, username, email } }` |
| POST | `/login` | No | `{ "email": string, "password": string }` | `200` → `{ message, token }` |

### Root

| Method | Endpoint | Auth | Input | Output |
|--------|----------|------|-------|--------|
| GET | `/` | No | — | `200` → `{ message: "Welcome to Restaurant APIs" }` |

### Restaurants

| Method | Endpoint | Auth | Input | Output |
|--------|----------|------|-------|--------|
| GET | `/restaurants` | No | — | `200` → array of restaurant objects |
| GET | `/restaurants/top` | No | — | `200` → array of top 5 restaurants sorted by rating (desc) |
| GET | `/restaurants/:id` | No | — | `200` → single restaurant object, or `404` if not found |
| POST | `/restaurants` | **Yes** | `{ "name": string, "city": string, "address": string, "cuisine": string, "rating": number }` | `201` → created restaurant object |
| PUT | `/restaurants/:id` | **Yes** | Any subset of the fields above | `200` → updated restaurant object, or `404` |
| DELETE | `/restaurants/:id` | **Yes** | — | `200` → `{ message: "Restaurant deleted successfully" }`, or `404` |

**Restaurant object shape:**
```json
{
  "_id": "ObjectId",
  "name": "string",
  "city": "string",
  "address": "string",
  "cuisine": "string",
  "rating": "number"
}
```

### Menu Items

| Method | Endpoint | Auth | Input | Output |
|--------|----------|------|-------|--------|
| GET | `/restaurants/:id/menu` | No | — | `200` → array of menu items for that restaurant |
| POST | `/restaurants/:id/menu` | **Yes** | `{ "name": string, "price": number, "isAvailable": boolean }` | `201` → created menu item, or `404` if restaurant doesn't exist |
| PUT | `/menu/:id` | **Yes** | Any subset of `name`, `price`, `isAvailable` | `200` → updated menu item, or `404` |
| DELETE | `/menu/:id` | **Yes** | — | `200` → `{ message: "Menu item deleted successfully" }`, or `404` |

**Menu item object shape:**
```json
{
  "_id": "ObjectId",
  "restaurantId": "ObjectId (ref: Restaurant)",
  "name": "string",
  "price": "number",
  "isAvailable": "boolean"
}
```
