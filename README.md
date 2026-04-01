### Docker hub
https://hub.docker.com/repository/docker/pritomssaha/601_module9/general

### Step
#### run the docker compose command
```bash
docker compose up --build
```
#### 1. Wait for starting all the dependency
#### 2. After container starts running, go to web browser, type localhost:5050, login to pgAdmin
<img src="/assets/pgadmin.PNG" />

#### create 2 table, one for users and another for calculations
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE calculations (
    id SERIAL PRIMARY KEY,
    operation VARCHAR(20) NOT NULL,
    operand_a FLOAT NOT NULL,
    operand_b FLOAT NOT NULL,
    result FLOAT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```
#### Now insert records into this 2 table
```sql
INSERT INTO users (username, email) 
VALUES 
('alice', 'alice@example.com'), 
('bob', 'bob@example.com');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES
('add', 2, 3, 5, 1),
('divide', 10, 2, 5, 1),
('multiply', 4, 5, 20, 2);
```
#### Retrive users and calculations data
```sql
SELECT * FROM users;
```
<img src="/assets/retrive_user.PNG" />

```sql
SELECT * FROM calculations;
```
<img src="/assets/retrive_calculation.PNG" />

#### Query both Users and calculations using join
```sql
SELECT u.username, c.operation, c.operand_a, c.operand_b, c.result
FROM calculations c
JOIN users u ON c.user_id = u.id;
```
<img src="/assets/join_sql.PNG" />

#### Update a record of calculations
```sql
UPDATE calculations
SET result = 6
WHERE id = 1;  -- or whichever row you want to update
```

#### Checks the record is updated
```sql
select * from calculations where id=1
```
<img src="/assets/update_calculation.PNG" />

#### Delete one record of user
```sql
DELETE FROM calculations WHERE id = 2; 
```

#### Checks the record is deleted

```sql
select *
from calculations
where id=2
```
<img src="/assets/delete_select.PNG" />
