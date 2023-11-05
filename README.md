# AWS_DMS_MSQ_TO_PG
Migrating MySQL to PostgreSQL With the AWS Database Migration Service, this is a cloudacademy lab


# ENVIROMENT BEFORE
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/bc8f5399-fb8e-47cc-9b4e-396cd6ebc212)

# ENVIROMENT AFTER
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/13289f0d-0892-4a1e-8645-856a26d3a001)

## Step 1

In the AWS search bar, enter Database Migration Service, and click the Database Migration Service result under Services:
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/3a4a558a-aa19-4f97-89f9-f2f876cefae4)

## Step 2

Create the endpoints, just click on endpoints in the left menu, might be under migrations

![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/f47a1473-f645-4ab2-af92-988f03598d9a)

This will populate the Endpoint configuration section of the form with values for Server name, Port, and User name.
- Mark provide access information manually, and input your password.

## Step 3 

Choose a vpc and test it

![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/2c3db597-98d3-4d41-bcfc-90984543cc84)

## Step 4 
Finally create the endpoint

## Step 5

Go to EC2 (I already have a instance running) and connect to your instance

![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/ecb7b10e-8c5a-43c2-b36e-91ddd6e31ccb)

![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/618fa207-739c-4f2b-a576-82c7b0e462e8)


## Step 6 

Get back to RDS and select your MySQL Databases
-Under the Connectivity & security heading, make a note of the Endpoint, it will be similar to the following:
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/e9336659-3d07-4f80-aec8-9f192406e540)

## Step 7

Aaaaaand back to EC2 where you got that beautiful file containing sample data to be loaded into the source database, mine is people.sql
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/974ad405-703f-4893-8598-1795fc59ed6d)

## Step 8

To load the people.sql data into the source database, enter the following command, replacing source-mysql-endpoint with the endpoint you noted down (I hope you did) earlier from RDS:
-use this:
"mysql -P <your-db-port> -u <your-db-username> -p -h "<source-mysql-endpoint>" < your-actual-filename.sql"

## Step 9
Connect to mysql and query some data to see if it's all there

## Step 10
FINALLY let's create the DMS task
-Go to DMS, while in there under Migrate data go to Database migration tasks and then, Create task:
-These are my configs
![image](https://github.com/nicholasloureiro/AWS_DMS_MSQ_TO_PG/assets/105894972/49f80850-f4e4-409f-96d9-868019ec6ea2)

The Migration type field allows you to specify different kinds of migration:

-Migrate existing data: This type is the simplest, it migrates data from the source to the target and finishes. Using this type will usually require an outage for the duration of the migration.
- Migrate existing data and replicate ongoing changes: This type will capture changes to the source during the migration and apply them. With this type outages can be minimized or avoided.
- Replicate data changes only: This type assumes you have already performed an initial migration of data from source to target, and want to migrate changes in the source that have occurred since. This allows for more complex migration scenarios, such as the initial migration happening outside of the AWS Database Migration Service.

## Step 11
On table mapping,, imagine you have a group of one or more database tables that don't have relationships with other tables. Selection rules can be configured to migrate those tables separately from the rest of the database, enabling you to migrate your database in parts. This approach may be less risky and easier to manage than migrating the entire database in one task.

## Step 12

Turn on premigration assessment, all of its options

## Step 13
Go back to the EC2 instance, choose your PG db, log in and check if the data is there
- psql -h "target-database-hostname" -U postgres -p 5432 people
- SELECT COUNT(*) AS row_count FROM people.people;

## Step 14
Be happy!







