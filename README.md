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
  <summary>Launch and Amazon RDS instance</summary>
  1. Navigate to the RDS console. <br>
  2. Select Databases and click create database. <br>
  3. Choose "Standard create" and the MariaDB engine type. <br>
  4. Keep the version provided by default and choose the Dev/Test template. <br>
  5. Use the following configurations: <br>
  - Instance identifier: my-database. <br>
  - Master username: admin. <br>
  - Master password: TheRQDword777! <br>
  - frrrrrtt
</details>

<details>
  <summary>Configure a Multi-AZ deployment</summary>
</details>

<details>
  <summary>Configure Amazon RDS backups</summary>
</details>

<details>
  <summary>Create a read replica of the primary database using a db.t3.xlarge instance</summary>
</details>
