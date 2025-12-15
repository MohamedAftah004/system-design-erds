# Maintenance & Service Request Management System

## Overview
This project represents a database and system design exercise for a maintenance and service request management system. The focus is on modeling real-world business rules, request lifecycle handling, approvals, technician assignment, and scalability.

The repository contains ERD designs created as part of practicing backend system design and data modeling.

---

## Actors

- Customer
- Technician
- Admin

---

## Core Requirements

### Customers

- Customers can register and manage their accounts
- Customers can store multiple addresses
- Customers can create maintenance service requests
- Customers can track the status of their requests
- Customers can rate completed services and leave feedback

---

### Maintenance Requests

- Each request belongs to a single customer
- A request includes:
  - Category
  - Priority
  - Description
  - Preferred date and time slot
  - Location selected from the customer’s saved addresses
- Requests support soft deletion

---

### Request Lifecycle

- Each request has a status that represents its current state
- Statuses are stored in a separate table (no enums)
- The design supports adding or modifying request states in the future
- Status changes are tracked in a request status history table

Example states include:
- Pending
- Approved
- Assigned
- In Progress
- Completed
- Cancelled

---

### Approval Flow

- Some requests require admin approval
- Admins can approve or reject requests
- Rejections may include a reason
- Approval actions are stored for auditing purposes

---

### Technicians

- Technicians can have one or more specialties
- Each technician has a status (e.g., active, unavailable)
- Technicians can be assigned to multiple requests
- Soft delete is supported

---

### Assignment

- A request can have one or more technicians assigned
- The system tracks:
  - Assigned technician
  - Assignment date
  - Whether the technician declined the assignment
- Implemented using a many-to-many relationship

---

### Scheduling

- Each request includes a scheduled date and time slot
- The schema supports future enforcement of technician availability rules

---

### Completion and Reviews

- Upon completion, technicians can submit:
  - Work report
  - Actual execution time
- Customers can:
  - Rate the service (1 to 5)
  - Leave textual feedback
- Reviews are linked to the request, customer, and technician

---

## Constraints and Design Decisions

- Request states are not implemented as enums
- All statuses are stored in dedicated tables
- Soft delete is applied to core entities
- The schema is designed to be extensible and production-ready

---

## Notes

- This project focuses on database and system design rather than implementation
- Some assumptions were made to keep the model realistic and scalable
- The ERD may evolve as additional business rules are introduced