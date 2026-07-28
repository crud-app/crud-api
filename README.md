# crud-api

A lightweight REST API built with **Rust** and **Axum**, backing a Student CRUD application. Handles create, read, update, and delete operations for student records, backed by PostgreSQL.

Pairs with the frontend repo: [`crud-app/student-frontend`](https://github.com/crud-app/student-frontend) 

## Tech Stack

- **[Axum](https://github.com/tokio-rs/axum)** — web framework
- **[Tokio](https://tokio.rs/)** — async runtime
- **[SQLx](https://github.com/launchbadge/sqlx)** — async PostgreSQL driver
- **[Serde](https://serde.rs/)** — JSON serialization
- **PostgreSQL** — database
- **tower-http (CORS)** — cross-origin support for the frontend

## API Endpoints

| Method | Route            | Description              |
|--------|------------------|--------------------------|
| GET    | `/health`        | Health check              |
| GET    | `/`              | Basic hello route          |
| GET    | `/students`      | Get all students          |
| POST   | `/students`      | Create a new student      |
| PUT    | `/students/{id}` | Update a student by ID    |
| DELETE | `/students/{id}` | Delete a student by ID    |

### Student model

```json
{
  "id": 1,
  "name": "John Doe",
  "age": 20
}
```

## Getting Started

### Prerequisites

- [Rust](https://www.rust-lang.org/tools/install) (2024 edition)
- PostgreSQL running locally or remotely

### Setup

1. **Clone the repo**
   ```bash
   git clone https://github.com/crud-app/crud-api.git
   cd crud-api
   ```

2. **Create a `.env` file** in the project root:
   ```env
   DATABASE_URL=postgres://<username>:<password>@localhost:5432/<db_name>
   PORT=3000
   ```

3. **Create the `students` table**
   ```sql
   CREATE TABLE students (
       id SERIAL PRIMARY KEY,
       name VARCHAR NOT NULL,
       age INTEGER NOT NULL
   );
   ```

4. **Run the server**
   ```bash
   cargo run
   ```

   The API will be available at `http://localhost:3000`.

### Quick test

```bash
curl http://localhost:3000/health
# OK

curl -X POST http://localhost:3000/students \
  -H "Content-Type: application/json" \
  -d '{"id": 1, "name": "John Doe", "age": 20}'
```

## Project Structure

```
crud-api/
├── src/
│   └── main.rs      # Routes, handlers, and server setup
├── Cargo.toml       # Dependencies
└── .env             # Local environment config (not committed)
```

## Roadmap

- [ ] Input validation (e.g. reject empty names, negative ages)
- [ ] Proper error handling instead of `.unwrap()` on DB calls
- [ ] Pagination on `GET /students`
- [ ] Automated tests
- [ ] Dockerfile for easier setup

## License

MIT
