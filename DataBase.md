# SESSION 7 : DATABASE

## Overview

In a typical setup like Gmail on EC2, the database is connected to the EC2 instance. Companies provide an `application server` that allows you to connect to a `database server`, but no direct link is provided to access your data.

## AWS Databases

AWS databases are managed services provided by the AWS cloud service provider. There are two types of services in managed services:

1. **Relational Database**
2. **Non-Relational Database**

### Relational Database

- **Hardware**: Managed by AWS
- **Operating System**: Managed by the customer
- **Database Software**: Includes both SQL and No-SQL

#### AWS SQL Softwares

Except for Amazon Aurora, all the following are unmanaged services where the customer should manage:

1. MySQL
2. Amazon Aurora
3. Microsoft SQL
4. PostgreSQL
5. MariaDB
6. Oracle

### Amazon RDS (Relational Database Service)

Amazon RDS is a managed service that makes it easy to set up, operate, and scale a relational database in the cloud. 

#### DB Instance Class

- **CPU**
- **Memory**
- **Network Performance**

#### DB Instance Storage

- **Magnetic**
- **General Purpose (SSD)**
- **Provisioned IOPS**

### Managed vs. Unmanaged Services

- **Unmanaged**: Scaling, fault tolerance, and availability are managed by you.
- **Managed**: Everything is managed by AWS. You manage only application optimization.

Managed services fall under the category of Software as a Service (SaaS).

## Key Points

- No direct connection to the database.
- Application server connects to the database server.


![Amazon RDS Architecture](https://github.com/user-attachments/assets/dc53b007-f9d4-47ae-8087-cae2ddb83c87)

- **DB Instance Class**: Shows the different performance parameters (CPU, Memory, Network Performance).
- **DB Instance Storage**: Different storage options available (Magnetic, SSD, Provisioned IOPS).


![Managed vs. Unmanaged Services](https://github.com/user-attachments/assets/f9e47025-1c89-40f4-95fb-fb30ed703102)

- **Unmanaged**: You manage scaling, fault tolerance, and availability.
- **Managed**: AWS manages everything; you focus only on application optimization.

## Definitions

- **Application Server**: A server that hosts applications and provides an environment for them to run.
- **Database Server**: A server that provides database services to other computer programs or computers.
- **RDS**: Amazon Relational Database Service, a managed relational database service by AWS.
- **SaaS**: Software as a Service, a software distribution model in which a third-party provider hosts applications and makes them available to customers over the Internet.

## Tables

| AWS SQL Software | Managed/Unmanaged |
| ---------------- | ----------------- |
| MySQL            | Unmanaged         |
| Amazon Aurora    | Managed           |
| Microsoft SQL    | Unmanaged         |
| PostgreSQL       | Unmanaged         |
| MariaDB          | Unmanaged         |
| Oracle           | Unmanaged         |

| DB Instance Storage   | Description                                    |
| --------------------- | ---------------------------------------------- |
| Magnetic              | Traditional magnetic storage                   |
| General Purpose (SSD) | Solid State Drive, general-purpose storage     |
| Provisioned IOPS      | High-performance storage with provisioned IOPS |
