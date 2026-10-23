# Salon Appointment Scheduler

A command-line salon appointment scheduler built with **Bash and PostgreSQL** as part of freeCodeCamp's **Relational Databases Certification**, under the *Build a Salon Appointment Scheduler* challenge.

The program interacts with customers through a terminal, displays available salon services, identifies existing customers by phone number, registers new customers, and records appointments in a PostgreSQL database.

## Features

- Display available salon services with their service IDs.
- Validate the selected service and prompt again when the selection is invalid.
- Identify existing customers using their phone numbers.
- Register new customers when their phone numbers are not found.
- Collect the requested appointment time.
- Store customer and appointment information in PostgreSQL.
- Use SQL queries to retrieve and insert database records.

## Technologies Used

- **Bash** — interactive command-line application
- **PostgreSQL** — relational database
- **SQL** — queries, table definitions, and constraints
- **psql** — PostgreSQL command-line client

## Repository Structure

```text
salon-appointment-scheduler/
├── salon.sh
├── salon.sql
└── README.md
```

| File | Description |
|---|---|
| `salon.sh` | Interactive Bash script for selecting services, identifying customers, and recording appointments. |
| `salon.sql` | PostgreSQL database dump containing the schema and sample data. |
| `README.md` | Project documentation and setup instructions. |

## Database Design

The database contains three related tables:

### `services`

Stores the salon services available for selection.

- `service_id` — unique identifier for each service.
- `name` — service name.

The current data includes five services: cut, color, perm, style, and trim.

### `customers`

Stores customer information.

- `customer_id` — unique customer identifier.
- `phone` — customer phone number, with a unique constraint.
- `name` — customer name.

### `appointments`

Stores appointment records.

- `appointment_id` — unique appointment identifier.
- `customer_id` — references the customer.
- `service_id` — references the selected service.
- `time` — requested appointment time.

Primary keys, a unique constraint on customer phone numbers, and foreign keys help maintain data integrity.

## How It Works

1. The program displays the available salon services.
2. The customer selects a service using its ID.
3. If the selected service does not exist, the program asks the customer to select again.
4. The program requests the customer's phone number and searches the database.
5. If the customer is new, the program asks for their name and saves their details.
6. The program asks for the requested appointment time.
7. The appointment is inserted into the database, and a confirmation message is displayed.

## Setup and Usage

### Prerequisites

- Bash shell
- PostgreSQL
- PostgreSQL command-line client (`psql`)
- A configured PostgreSQL role with access to the `salon` database

### 1. Clone the repository

```bash
git clone https://github.com/Adarsha-o-O/salon-appointment-scheduler.git
cd salon-appointment-scheduler
```

### 2. Restore the database

**Warning:** The `salon.sql` dump contains commands to drop and recreate the `salon` database. Running it may permanently delete an existing database with that name. Inspect the file and back up any important data before restoring it.

To restore the dump using a PostgreSQL administrator role:

```bash
psql -U postgres -d postgres -f salon.sql
```

The dump assigns database ownership to the `freecodecamp` role. Make sure the role exists and that the restoring user has the required permissions.

### 3. Configure database access

The script connects to PostgreSQL using:

```bash
psql --username=freecodecamp --dbname=salon --no-align --tuples-only -c
```

Ensure that the `freecodecamp` role exists and can connect to the `salon` database and perform the required queries and inserts.

If your local PostgreSQL configuration differs, update the connection settings in `salon.sh`.

### 4. Make the script executable

On Linux or another compatible Bash environment, run:

```bash
chmod +x salon.sh
```

### 5. Run the program

```bash
./salon.sh
```

Follow the prompts to select a service, enter a phone number, provide a name if you are a new customer, and specify an appointment time.

## Example Interaction

The following is an illustrative example of the interaction:

```text
~~~~~ MY SALON ~~~~~

Welcome to My Salon, how can I help you?

1) cut
2) color
3) perm
4) style
5) trim

1

What's your phone number?
555-123-4567

I don't have a record for that phone number, what's your name?
Alex

What time would you like your cut, Alex?
10:30

I have put you down for a cut at 10:30, Alex.
```

The actual output depends on the services and customer data in the database.

## What I Learned

Through this project, I practiced:

- Building an interactive command-line application with Bash.
- Using command-line arguments and variables.
- Reading user input and validating selections with loops.
- Using conditional statements to handle existing and new customers.
- Connecting Bash scripts to PostgreSQL with `psql`.
- Writing SQL queries to retrieve and insert records.
- Designing relational tables with primary keys, unique constraints, and foreign keys.
- Linking customers, services, and appointments through database relationships.
- Exporting a PostgreSQL database to an SQL dump for submission.

## Learning Context

This project was completed as part of the **freeCodeCamp Relational Databases Certification**.

Challenge: [Build a Salon Appointment Scheduler — freeCodeCamp](https://www.freecodecamp.org/learn/relational-databases/)

The repository contains the two required challenge files: `salon.sh` and `salon.sql`.

## Future Improvements

- Validate phone numbers and appointment times more thoroughly.
- Use safer SQL parameter handling instead of inserting raw user input into query strings.
- Add appointment listing, cancellation, and rescheduling features.
- Improve database connection configuration and error handling.
- Add automated tests for invalid inputs and database operations.

---

**Author:** [Adarsha-o-O](https://github.com/Adarsha-o-O)

