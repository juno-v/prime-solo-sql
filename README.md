# prime-solo-sql


## Base Mode Questions
1. How do you get all users from Chicago?
2. How do you get all users with usernames that contain the letter a?
3. The bank is giving a new customer bonus! How do you update all records with an account balance of 0.00 and a transactions_attempted of 0? Give them a new account balance of 10.00.
4. How do you select all users that have attempted 9 or more transactions?
5. How do you get the username and account balance of the 3 users with the highest balances, sorted highest to lowest balance? NOTE: Research LIMIT
6. How do you get the username and account balance of the 3 users with the lowest balances, sorted lowest to highest balance?
7. How do you get all users with account balances that are more than $100?
8. How do you add a new account?
9. The bank is losing money in Miami and Phoenix and needs to unload low transaction customers: How do you delete users that reside in miami OR phoenix and have completed fewer than 5 transactions.

## Stretch Goal Questions (word problems)
1. Anthony moved to Santa Fe.
2. Grace closed her account.
3. Travis made a withdrawl of $20,000. What's their new balance? NOTE: Research RETURNING
4. The Bank needs to track last names. NOTE: Research ALTER TABLE https://www.postgresql.org/docs/10/static/sql-altertable.html


CREATE TABLE accounts (
    user_id serial PRIMARY KEY,
    username varchar(12) NOT NULL,
    city varchar(128),
    transactions_completed integer,
    transactions_attempted integer,
    account_balance numeric(12,2)
);

INSERT INTO accounts (username, city, transactions_completed, transactions_attempted, account_balance) VALUES ('shawn', 'chicago', 5, 10, 355.80);,
('cherise', 'minneapolis', 9, 9, 4000.00),
('larry', 'minneapolis', 3, 4, 77.01),
('dallas', 'new york', 6, 12, 0.99),
('anthony', 'chicago', 0, 0, 0.00),
('travis', 'miami', 10, 100, 500000.34),
('davey', 'chicago', 9, 99, 98.04),
('ora', 'phoenix', 88, 90, 3.33),
('grace', 'miami', 7, 9100, 34.78),
('hope', 'phoenix', 4, 10, 50.17);

-- BASE GOALS 

-- 1. How do you get all users from Chicago?
	SELECT "username" FROM "accounts"; 
	
-- 2. How do you get all users with usernames that contain the letter a?
	SELECT "username" FROM "accounts" WHERE "username" LIKE '%a%'; 

-- 3. The bank is giving a new customer bonus! How do you update all records with an account balance of 0.00 and a transactions_attempted of 0? Give them a new account balance of 10.00.
	-- let's find all records with account balance = 0.00 AND transactions_attemped = 0
	SELECT * FROM "accounts" WHERE "account_balance" = 0.00 AND "transactions_attempted" = 0;
	-- update record 
	UPDATE "accounts" SET "account_balance" = 10.00 WHERE "user_id" = 5;
	
-- 4. How do you select all users that have attempted 9 or more transactions?
	SELECT "username", "transactions_attempted" FROM "accounts" WHERE "transactions_attempted" >= 9;
	
-- 5. How do you get the username and account balance of the 3 users with the highest balances, sorted highest to lowest balance? NOTE: Research LIMIT
	SELECT "username", "account_balance" FROM "accounts" ORDER BY "account_balance" DESC LIMIT 3;

-- 6. How do you get the username and account balance of the 3 users with the lowest balances, sorted lowest to highest balance?
	SELECT "username", "account_balance" FROM "accounts" ORDER BY "account_balance" ASC LIMIT 3; 
	
-- 7. How do you get all users with account balances that are more than $100?
	SELECT "username", "account_balance" FROM "accounts" WHERE "account_balance" > 100;
	
-- 8. How do you add a new account?
	-- I added myself as an account. 
	INSERT INTO accounts (username, city, transactions_completed, transactions_attempted, account_balance) VALUES('juno', 'saint paul', '1000', '1000', '1000');

-- 9. The bank is losing money in Miami and Phoenix and needs to unload low transaction customers
-- : How do you delete users that reside in miami OR phoenix and have completed fewer than 5 transactions.
	SELECT "username", "city" FROM "accounts" WHERE "city" LIKE '%miami%' OR "city" LIKE '%phoenix%';


-- STRETCH GOALS 

-- 1. Anthony moved to Santa Fe.

	-- find anthony (ILIKE) disregards any lower/uppercase sensitivity. 
SELECT "username", "user_id" FROM "accounts" WHERE "username" ILIKE '%Anthony%';
	-- UPDATE anthony's city
	UPDATE "accounts" SET "city" = 'Santa Fe' WHERE "user_id" = 5;
	
-- 2. Grace closed her account.
	DELETE FROM "accounts" WHERE "user_id" = 9;
	
-- 3. Travis made a withdrawl of $20,000. What's their new balance? NOTE: Research RETURNING
		
		
-- 4. The Bank needs to track last names. NOTE: Research ALTER TABLE https://www.postgresql.org/docs/10/static/sql-altertable.html