## Pepper
1. Strong String that is appended to every password
2. String is complex and long (100 chars)
3. Stored in variable environment or vault, separate from DB

## Salt
1. Adding random string to every password
2. Each instance is unique for every password
3. Stored together with passwords in database

## Process

**Hashfunction (PW + PEPPER + SALT) --> SALT:HashOfPW**
