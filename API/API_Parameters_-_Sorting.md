# Sorting

Examples: 

### Single Sort

```
GET /users?sort_by=asc(email) and GET /users?sort_by=desc(email)

GET /users?sort_by=+email and GET /users?sort_by=-email

GET /users?sort_by=email.asc and GET /users?sort_by=email.desc

GET /users?sort_by=email&order_by=asc and GET /users?sort_by=email&order_by=desc
```


### Multi Sort

```
GET /users?sort_by=desc(last_modified),asc(email) or 
GET /users?sort_by=-last_modified,+email
```

## Resource(s)
- REST API Design Filtering Sorting & Pagination
