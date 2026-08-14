# Contracts Lab

A small Flask API for a company that manages contracts between two parties. It exposes two read-only endpoints: one for contract details and one for confirming a customer exists, without exposing any of their data.

## Routes

### `GET /contract/<id>`

Looks up a contract by integer `id` in the in-memory `contracts` list.

- **200 OK** — contract found; response body is the contract's `contract_information` string.
- **404 Not Found** — no contract with that id.

Example:
```
GET /contract/1
200 OK
This contract is for John and building a shed
```
```
GET /contract/100
404 Not Found
```

### `GET /customer/<customer_name>`

Checks whether `customer_name` is present in the in-memory `customers` list. Customer data is sensitive, so the response never includes any information — it only confirms existence.

- **204 No Content** — customer found; response body is empty.
- **404 Not Found** — no customer with that name.

Example:
```
GET /customer/bob
204 No Content
```
```
GET /customer/mario
404 Not Found
```

## Data

Contracts and customers are hardcoded in `server/app.py`:

```python
contracts = [
    {"id": 1, "contract_information": "This contract is for John and building a shed"},
    {"id": 2, "contract_information": "This contract is for a deck for a buisiness"},
    {"id": 3, "contract_information": "This contract is to confirm ownership of this car"},
]
customers = ["bob", "bill", "john", "sarah"]
```

## Setup

```
pipenv install
pipenv shell
```

## Running the app

```
cd server
python app.py
```

The server runs at `http://localhost:5555`.

## Running tests

```
pytest server/testing/app_test.py -v
```
