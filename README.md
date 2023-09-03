# Improvement of RDS Instances in AWS
Improved the operational efficiency, availability and performance of relational databases by using multiple AZs and a read replica.

## Architecture Diagram

![Screenshot 2023-09-03 at 10 30 28](https://github.com/martins-jean/Improvement-of-RDS-Instances-in-AWS/assets/118685801/beee3609-0866-4f41-aa43-5e8164efbdc5)

## Project Overview

1. This solution uses Amazon RDS, which is fully managed and removes the need for manual database infrastructure provisioning and maintenance. <br>
2. Amazon RDS automates backups, database snapshots, and host replacement to reduce the administrative burden. <br>
3. To achieve high availability, I deployed the database across multiple availability zones. In a Multi-AZ deployment, Amazon RDS automatically creates a primary DB instance and synchronously replicates the data to an instance in a different AZ. <br>
4. When RDS detects a failure, it automatically fails over to a standby instance in a different AZ, without manual intervention. <br>
5. As the name record for your DB instance remains the same, your application can resume database operations without the need for further intervention by the user. <br>
6. For read-heavy database workloads, you can create one or more read replicas of a DB instance. This way, you can serve high-volume application read traffic from multiple copies of your data, thereby increasing its aggregate read throughput. <br>

## Reproducibility Guidelines

<details>
  <summary>Required setup</summary>
  1. Create a VPC with DNS resolution and hostnames enabled. <br>
  2. Create a security group that allows all traffic, all protocols and all port ranges for both inbound and outbound rules and name it default. <br>
</details>

<details>
  <summary>Launch and Amazon RDS instance</summary>
  1. Navigate to the RDS console. <br>
  2. Select Databases and click create database. <br>
  3. Choose "Standard create" and the MariaDB engine type. <br>
  4. Keep the version provided by default and choose the Dev/Test template. <br>
  5. Use the following configurations: <br>
  - Instance identifier: my-database. <br>
  - Master username: admin. <br>
  - Master password: TheRQDword777! <br>
  - DB instance class: Burstable classes. <br>
  - Type: db.t3.xlarge <br>
  - Storage type: General purpose SSD (gp2). <br>
  - Allocated storage: 20. <br>
  - Enable storage autoscaling: checked. <br>
  - Maximum storage threshold: 1000. <br>
</details>

<details>
  <summary>Configure a Multi-AZ deployment</summary>
  1. Under Availability and Durability, Multi-AZ deployment: Create a standby instance. <br>
  2. Continue the creation with the following configurations:
  - VPC: keep the default VPC. <br>
  - Subnet: default. <br>
  - Public access: no. <br>
  - VPC security group: choose existing, then default. <br>
  - Database authentication options: password authentication. <br>
  - Under monitoring, turn on performance insights. <br>
  - Expand additional configuration if needed and clear the enhanced monitoring checkbox. <br>
</details>

<details>
  <summary>Configure Amazon RDS backups</summary>
  1. Under database options, use the following configurations: <br>
  - Initial database name: my_database. <br>
  - DB parameter group: default.mariadb10.6 <br>
  - Option group: default:mariadb-10-6 <br>
  2. Under backup, choose the following: <br>
  - Automated backups: enabled. <br>
  - Backup retention period: 7 days. <br>
  - Backup window: no preference. <br>
  3. Under encryption choose the following:
  - Enable encryption: checked. <br>
  - Enable auto minor version upgrade: cleared. <br>
  - Maintenance window: no preference. <br>
  4. Click on create database. <br>
</details>

<details>
  <summary>Create a read replica of the primary database using a db.t3.xlarge instance</summary>
  1. After the creation of the database is finished which should take between 15 and 20 minutes, refresh until the status is listed as available. <br>
  2. Click on Actions and then Create read replica. <br>
</details>
