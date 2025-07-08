# Module 8: API Development with FastAPI

A module of is601 Web Systems Development, by Keith Williams

This module introduces pgadmin, Postgres RDBMS, and general SQL to the CI/CD environment, but does not yet implement an ORM or history functionality into the web calculator.

7/8/2025-5pm. a Docker Hub internal issue is preventing the creation of new Repositories:
![Screenshot 2025-07-08 142854](https://github.com/user-attachments/assets/ba4a05fa-0a4d-4ffc-b140-25d55d8cd9ee)

If this issue is resolved before Module 9 is due, the proper environment variables and repository link will be added to this readme.

## Reflection Portion

I really love working with database systems and have built apps with mariadb and postgres in the past (and mongodb currently,) so the real boon of this module was the introduction of pgadmin and volumes in docker compose. How to maintain and modify a persistant backend on a remote machine really felt like the last gap in my experience with basic containerization, so I expect the upcoming module to be quite fruitful. I'm interested too in seeing an ORM (and perhaps a database migration) executed in a Python environment, as I have only built these services using Go, and only for one project.

## Screenshots

### Docker Compose Output

![Screenshot 2025-07-08 175850](https://github.com/user-attachments/assets/b3bbb8ba-ae4b-4377-99b3-f67a84b7b5c3)
![Screenshot 2025-07-08 175906](https://github.com/user-attachments/assets/902015fe-8d49-4bde-8304-ab79c0d8e093)
![Screenshot 2025-07-08 175936](https://github.com/user-attachments/assets/0f0dc800-6982-482c-b245-e265baf8cdb9)

### Docker Teardown

![Screenshot 2025-07-08 130732](https://github.com/user-attachments/assets/d1f79d88-902e-4a39-a61b-50db1f379dc6)

## SQL Operations

### A. Create Tables -- Users and Calculations

![Screenshot 2025-07-06 090710](https://github.com/user-attachments/assets/7cdd18f7-6b5b-4c72-b302-e81914d8d190)

![Screenshot 2025-07-08 123920](https://github.com/user-attachments/assets/fe1f5d73-db1b-4607-972a-729e4d8df70a)

Note the establishment of user_id as a foreign key on Users, using that table's id field.

### B. Inserting Test Records

![Screenshot 2025-07-08 124001](https://github.com/user-attachments/assets/c08e366d-a37d-4839-a3d7-21e173f37cf3)

![Screenshot 2025-07-08 124025](https://github.com/user-attachments/assets/2ccc1d70-1bb7-47b8-9bc0-07ddeef2ed25)

Note the numeric user_id field in Calculation entries. User.id is a simple incrementing ID, so 1 = alice, 2 = bob, 

### C. Unfiltered Table Queries

![Screenshot 2025-07-08 124103](https://github.com/user-attachments/assets/a839692b-b392-4aa9-9db6-672f13e314cd)

![Screenshot 2025-07-08 124136](https://github.com/user-attachments/assets/d090770d-30e7-4bc9-b4bc-d3919853b909)

Here we see the full tables, consisting of the records we've just inserted. 

### C. Simple Joined Query

![Screenshot 2025-07-08 124205](https://github.com/user-attachments/assets/81f6f26c-b12d-468d-be98-22fe89b3fbe1)

Note: My original education in SQL had me using "SELECT x FROM (Some subquery on tablea, tableb) WHERE" instead of JOIN x ON

### D. Simple Update

![Screenshot 2025-07-08 124239](https://github.com/user-attachments/assets/5689972d-a3ea-4d1c-aca5-446a897aec76)

This is pretty straightforward. Calculation 1 (add 2 + 3) is now 2 + 3 = 6. Surely this will turn out fine.

### E. Simple Delete

![Screenshot 2025-07-08 124320](https://github.com/user-attachments/assets/d2300c4b-cec7-4018-830a-9f80647bc446)

Note the 'id' field specified here is the Primary Key of the Calculations table, not a user_id. This way only one record is ever deleted.

### Bonus. Simple Cleaning Operation

![Screenshot 2025-07-08 124549](https://github.com/user-attachments/assets/5aaa53c7-d4b2-44d7-8b3d-b00abd8cc457)

It's not recommended that DELETE or UPDATE statements be built such that they can theoretically affect more than one entry, but I thought I would present an example query to clean out invalid adds, since we made one in part D.

### Bonus. Simple History Clear

![Screenshot 2025-07-08 130215](https://github.com/user-attachments/assets/217ad077-5fc9-482c-80f7-94fff8479add)

I imagine this sort of operation would use a cookie or other authentication value to match to a user first before deleting that user's records, but this works for an academic example where we have our unique username and not our user id.






