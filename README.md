# Test Task: Sem Shekhovtsov

## package references fixes

- for the frontend application - simply with npm audit fix
- for the backend application, some packages are removed and missing are added:

removed following unused, incompatible libraries: 
	"js2xml": "^1.0.9"
	"xmldom": "^0.6.0"
added missing library:
	"request": "^2.88.2"

fixed package references with:
	npm audit fix --force

## Loan application form fix

- added missing BForm element scripts
- moved the buttons inside the form to be able to submit the form ;)
- added applications form live refresh -> events handling
- added form reset after submission
- fixed the outgoing_mortgage database table column name
- fixed saving the Loan Application into the database -> by adding the @IsString attribute
- added the aboveAverage boolean flag to the POST action response

<!-- omit in toc -->
# Bridgit competency test

Welcome to the Bridgit technical test. There are three tasks of increasing complexity. After you have set up the software complete as many tasks as you can in the allotted timeframe.

| Project  | Description                                |
|----------|--------------------------------------------|
| Database | PostgreSQL managed by Sequelize Migrations |
| Backend  | NodeJS/Typescript with NestJS framework    |
| Frontend | VueJS/Typescript                           |

<!-- omit in toc -->
### Table of contents

- [Setting up](#setting-up)
- [Task - Submit loan application](#task---submit-loan-application)

![Broker portal](broker-portal.png "Broker portal")

## Setting up

Prerequisites: 

- NodeJS 16
- Docker

Setting up the database on `postgres://user:password@localhost:5436/technical_test`:

```bash
# start postgresql server using Docker's "Compose"
$ docker-compose up -d 
# create and populate the database using Sequelize
$ cd database
$ cp .env.localdev .env
$ npm install
$ npm run build
$ npm run migrate
$ npm run seed:all
```

Setting up the backend on `http://localhost:7100` with Swagger on `http://localhost:7100/swagger`:

```bash
$ cd backend
$ cp .env.localdev .env
$ npm install
$ npm run start:dev
```

Setting up the frontend on `http://localhost:7200`:

```bash
$ cd frontend
$ cp .env.localdev .env
$ npm install 
$ npm run start:dev
```

Log in to the frontend as broker 1. You can find the login information in the database seeder script.

## Task - Submit loan application
Create the functionality for a broker to submit a new loan application.

  1. Show a modal after clicking the "Submit application" button, and allow the broker to enter the following information:
   
        - applicant_name
        - applicant_email
        - applicant_mobile_phone_number
        - applicant_address
        - annual_income_before_tax
        - incoming_address
        - incoming_deposit
        - incoming_price
        - incoming_stamp_duty
        - loan_amount
        - loan_duration
        - monthly_expenses
        - outgoing_address
        - outgoing_mortgage
        - outgoing_valuation
        - savings_contribution
  
  2. Add a backend endpoint to receive the application submission
  3. Query all existing applications and get the average `loan_amount`
  4. Save the new application to the `applications` table
  5. Return if new loan's loan_amount is above or below the average

Commit your code to your personal git and share the link with us.