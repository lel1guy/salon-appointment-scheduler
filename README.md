# 💈 Salon Appointment Scheduler

> **freeCodeCamp Relational Database Certification — Project #3**

A terminal-based interactive appointment booking system built with **PostgreSQL** and **Bash**. Customers can browse services, check in by phone number, and schedule appointments — all through a clean CLI menu.

---

## ✨ Features

- **Interactive menu** — displays available services loaded directly from the database
- **Input validation** — rejects invalid service selections and re-prompts until valid
- **Customer auto-registration** — recognizes returning customers by phone number; creates new records on first visit
- **Appointment booking** — links customers, services, and appointment times with proper foreign key relationships
- **Self-contained script** — single `salon.sh` file handles the full flow via `psql`

## 🛠️ Technologies

| Tech | Purpose |
|------|---------|
| **PostgreSQL** | Relational database (3 tables: `customers`, `services`, `appointments`) |
| **Bash** | Scripting language for the interactive CLI |
| **psql** | PostgreSQL's native CLI client |

## 🗄️ Database Schema

```
salon
├── customers
│   ├── customer_id  SERIAL PRIMARY KEY
│   ├── name         VARCHAR NOT NULL
│   └── phone        VARCHAR NOT NULL UNIQUE
├── services
│   ├── service_id   SERIAL PRIMARY KEY
│   └── name         VARCHAR NOT NULL
└── appointments
    ├── appointment_id  SERIAL PRIMARY KEY
    ├── customer_id     INT → customers(customer_id)
    ├── service_id      INT → services(service_id)
    └── time            VARCHAR NOT NULL
```

## 🚀 How to Run

```bash
# 1. Create the database
psql -U postgres -c "CREATE DATABASE salon;"

# 2. Connect and create tables
psql -U postgres -d salon -f salon.sql

# 3. Run the scheduler
chmod +x salon.sh
./salon.sh
```

### Sample session

```
~~~~~ MY SALON ~~~~~

Welcome to My Salon, how can I help you?

1) cut
2) color
3) perm
4) style
5) trim
1

What's your phone number?
555-555-5555

I don't have a record for that phone number, what's your name?
Fabio

What time would you like your cut, Fabio?
10:30

I have put you down for a cut at 10:30, Fabio.
```

Returning customers skip the name prompt — the script recognizes them by phone number.

## 📦 Files

| File | Description |
|------|-------------|
| `salon.sh` | The interactive bash script |
| `salon.sql` | PostgreSQL dump (schema + data + constraints) |
| `README.md` | This file |

## 🏁 Certification

This project is part of **freeCodeCamp's Relational Database Certification**.
