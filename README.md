# LARAVEL JOB OPENINGS REST API

A LARAVEL based RESTful API with the following features:

* Recruiter Registration/Login, where each recruiter belongs to a different company;
* CRUD of vacancies by recruiters;
* Jobs have the fields: title, description, status, address, salary, company;
* A recruiter cannot modify jobs created by another;
* Public listing of open positions;
* Public search for open positions;
* Search criteria that must be accepted: keyword, address, salary, company.

### Starting

These instructions provide a working copy of the project on your local machine for development and testing purposes. Read the following content to install and allow the application to work.

### Requirements

First you need to have composer installed on your machine: [https://getcomposer.org/download/](https://getcomposer.org/download/)

With the composer already installed, download the repository:

```
git clone https://github.com/eidercarlos/backend-careers.git
```

### Installing

Have Laravel installed on your machine:

```
composer global require laravel/installer
```

Install/update the dependencies:

```
composer update
```

Then, from the .env.example file create a new file with the extension .env and configure the local settings of your MySQL database.

``` 
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=jobopenings_api
DB_USERNAME=root
DB_PASSWORD=

```

Don't forget to have a database created with the same name you have in your .env file MySQl DB Connection configuration (jobopenings_api).


Don't forget to also generate a KEY for your application.

```
php artisan key:generate
```

If there is no issue when triggering the command below, it means that the application is OK.

```
php artisan serve
```

Now let's migrate our database tables and also populate with some records:

```
php artisan migrate:fresh --seed
```

If all the steps above were successful, we have our REST API working.

Unit tests can be executed with the following command:

```
php artisan test
```

## Main Files/Classes

### API EndPoints (routes)

* api.php

To access the API don't forget to run the following command

```
php artisan serve
```

To access the protected endpoints, it is important to log in first
and the token for access will be returned.
If you run the command to populate the database with some records, you can also use the following data
for login and password in the api:

```
POST http://localhost:8000/api/login
form-data:
  login: admin
  password: laraveljobsapi
```

Then just add the token in the Authorization -> Bearer Token section of Postman for example,
to be able to test the requests that require authorization.


#### PUBLIC EndPoints

* Recruiter

Login
```
POST http://localhost:8000/api/login
form-data:
  login: ???
  password: ???
```

* Job

Get all jobs:
```
GET http://localhost:8000/api/jobs
```

Get all open jobs
```
GET http://localhost:8000/api/openjobs
```

Get a specific job opening
```
GET http://localhost:8000/api/jobs/{#id}
```  

Filtering the jobs by keyword, address, salary, company:
```
POST http://localhost:8000/api/jobsfilter
form-data:
  keyword: ???
  address: ???
  salary: ???
  company: ???
```


#### PROTECTED EndPoints

* Recruiter

Create a new user (Recruiter):
```
POST http://localhost:8000/api/register
form-data:
  id_company: #1
  name: ???
  login: ???
  password: ???
```

API Logout:
```
POST http://localhost:8000/api/logout
```

* Company

Get all companies:
```
GET http://localhost:8000/api/companies
```

Get a specific company:
```
GET http://localhost:8000/api/companies/{#id}
```

Create a company:
```
POST http://localhost:8000/api/companies
form-data:
  name: ???
```

*  Job

Create a job opening:
```
POST http://localhost:8000/api/jobs
form-data:
  'title': ???
  'description': ???
  'address': ???
  'salary': ???
  'company': ???
```

Update a job opening:
```
PUT http://localhost:8000/api/jobs/{#id}
form-data:
  'title': ???
  'description': ???
  'address': ???
  'salary': ???
  'company': ???
```

Delete a job opening:
```
DELETE http://localhost:8000/api/jobs/{#id}
```


### Model classes (app -> Models)

* Company.php
* Job.php
* Recruiter.php

### Controller classes (Http -> Controllers)

* CompanyController.php
* JobController.php
* RecruiterController.php

### Unit Testing classes (tests -> Feature)

* CompanyApiTest.php
* JobApiTest.php
* RecruiterApiTest.php