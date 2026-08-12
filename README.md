# PC Service Portal

A full-stack PC Service Management System built with:

- Go
- Gin
- MongoDB
- React

Features

- Customer Portal
- Technician Dashboard
- Device Management
- Job Tracking
- Authentication
- Role Based Access

## .env file

```

MONGO_URI=mongodb://mongo:27017
MONGO_DB_NAME=<database-name>

PORT=6543

JWT_SECRET=<change-this-to-a-long-random-secret>
JWT_EXPIRY_HOURS=24

GIN_MODE=release

ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173

```



### Initial System Setup

1. Open http://localhost:3000/
2. Register account with email and password. That account will be registered as customer.
3. Now run 


```
docker exec -it pc-support-mongo mongosh

```

```
use <dbname mentioned in env file>

```

```
db.users.find(
  {},
  { email: 1, role: 1 }
).pretty()

```
enter correct email

```
db.users.updateOne(
  { email: "test@example.com" },   
  { $set: { role: "super_admin" } }
)
```
Get confimation message

`{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
`
Exit the promt "exit"

4. Log in again.
5. Create the Admin account.
6. Use the Admin account for all business operations.

