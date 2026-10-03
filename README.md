# EventForce Management System

A Salesforce CRM-based Event Management System designed to centralize and automate event planning activities such as client management, venue booking, vendor coordination, cancellations, feedback, reminders, and reporting.

## Project Overview

EventForce helps event planning teams manage their operations through a single Salesforce platform. The system connects Events, Clients, Venues, Vendors, Feedback, and Event Vendors using a structured data model.

The application uses Salesforce automation, Apex, approval processes, security controls, reports, and dashboards to reduce manual work and improve event coordination.

## Objectives

- Centralize event, client, venue, vendor, and feedback information.
- Prevent venue double booking on the same date.
- Automatically update venue availability.
- Send client reminders three days before an event.
- Manage event cancellation through an approval process.
- Provide role-based access control.
- Provide reports and dashboards for monitoring upcoming events.
- Maintain accurate and consistent event data.

## Technologies Used

| Technology / Feature | Purpose |
|---|---|
| Salesforce CRM | Main development platform |
| Salesforce Developer Edition | Development environment |
| Custom Objects | Store project data |
| Salesforce Flow | Automated client reminders |
| Approval Process | Event cancellation approval |
| Apex | Business logic and automation |
| Apex Triggers | Venue status and double-booking validation |
| Batch Apex | Complete past events automatically |
| Schedulable Apex | Schedule batch processing |
| Validation Rules | Data validation |
| Lightning App | User interface |
| Reports & Dashboards | Event monitoring and analytics |
| Data Import Wizard | Data migration |
| Profiles & Roles | Access control |
| Permission Sets | Additional permissions |

## Data Model

The system contains six custom objects:

1. Event
2. Client
3. Vendor
4. Venue
5. Feedback
6. Event Vendor - Junction object

### Relationships

```text
Client ────────────< Event >──────────── Venue
                       |
                       v
                  Event Vendor
                   /       \
                  /         \
              Event         Vendor

Client ────────────< Feedback >────────── Event
```

The Event Vendor junction object provides a many-to-many relationship between Events and Vendors.

## Key Features

### 1. Event Management

Users can create and manage events with:

- Event Name
- Client
- Venue
- Event Date
- Event Type
- Event Status
- Event Budget

Supported event types include Wedding, Corporate, Birthday, Anniversary, Festival, Concert, and Other.

### 2. Client Management

Client records contain:

- Client Name
- Phone
- Email
- Address
- City
- Country

An email validation rule prevents invalid email addresses from being saved.

### 3. Venue Management

Venue information includes:

- Venue Name
- Address
- Location
- Capacity
- Availability Status

Venue availability can be:

- Available
- Reserved
- Not Available

### 4. Vendor Management

Vendor records contain:

- Vendor Name
- Phone
- Email
- Service Type
- Status

Services include catering, decoration, photography, videography, lighting, stage setup, transportation, hosting, and more.

### 5. Double-Booking Prevention

The `PreventDoubleBooking` Apex trigger checks whether another event already uses the same venue on the same date.

Error message:

```text
This Venue is already booked on this date.
```

### 6. Automatic Venue Status

`VenueStatusHelper` automatically updates venue availability:

```text
Event Status = Confirmed
        ↓
Venue = Reserved
```

```text
Event Status = Canceled
        ↓
Venue = Available
```

### 7. Client Reminder

The `Client Reminder - 3 Days Before` Record-Triggered Flow sends an automated reminder to the client three days before a confirmed event.

The reminder contains:

- Client name
- Event name
- Event date
- Venue
- Event type

### 8. Cancellation Approval

Event cancellations are controlled through the `Event_Cancellation_Process` Approval Process.

```text
Pending Cancellation
        ↓
Manager Review
        ↓
 ┌──────┴──────┐
 ▼             ▼
Approve       Reject
 │             │
 ▼             ▼
Canceled      Rejected
```

The process includes record locking, manager approval, field updates, and email notifications.

### 9. Automatic Event Completion

The system uses Batch Apex to find past events that are not marked as Completed.

```text
Past Event
    ↓
BatchCompleteEvents
    ↓
Event Status = Completed
```

`ScheduleCompleteEvents` schedules the batch job to run automatically.

### 10. Feedback Management

Clients can provide feedback for events using:

- Rating
- Comments
- Client
- Event

A lookup filter ensures that the selected event belongs to the selected client.

## Reports & Dashboard

### Reports

- New Events with Venue Report
- Upcoming Events by Month

### Dashboard

**EventForce Operations Dashboard**

The dashboard provides a quick overview of upcoming events using report data.

## Security

The system uses:

- Profiles
- Roles
- Permission Sets
- Organization-Wide Defaults
- Sharing Rules

### Profiles

- Event Admin
- Event Coordinator
- Vendor Manager
- Client Profile

A `Feedback Manager` permission set provides additional permissions for feedback management.

## Event Workflow

```text
Client Registration
        ↓
Event Planning
        ↓
Venue Selection
        ↓
Vendor Assignment
        ↓
Event Confirmation
        ↓
Automated Reminder
        ↓
Event Execution
        ↓
Feedback
        ↓
Event Completion
```

Cancellation workflow:

```text
Cancellation Request
        ↓
Manager Approval
        ↓
Approved / Rejected
        ↓
Status Update + Email Notification
```

## Testing

The project includes test cases for:

- Email validation
- Venue double-booking prevention
- Venue reservation
- Venue availability
- Cancellation approval
- Cancellation rejection
- Client reminder Flow
- Batch event completion
- Access control
- Sharing rules

## Development Methodology

The project followed an Agile development approach with four sprints.

| Sprint | Story Points | Main Work |
|---|---:|---|
| Sprint 1 | 8 | Event, Client & Venue Management |
| Sprint 2 | 8 | Vendor Management & Notifications |
| Sprint 3 | 13 | Approval & Apex |
| Sprint 4 | 10 | Security & Reports |

**Total:** 39 story points across 8 user stories.

## Team

**Team ID:** `SWTID-2026-3509`

| Name | Role |
|---|---|
| Naveen P | Team Leader |
| Saravanan K | Team Member |
| Roopan G | Team Member |
| Mukil Doss S | Team Member |

**Institution:** St. Joseph's College of Engineering and Technology, Thanjavur  
**College Code:** 8219

## Future Enhancements

- Production deployment using Salesforce sandboxes and deployment tools.
- Improved booking using time slots and overlapping-date checks.
- Multi-step approval and escalation.
- Vendor performance management.
- Additional analytics for vendors, feedback, and budgets.
- SMS/WhatsApp integrations.
- Improved mobile experience.
- Apex test classes and production-level code coverage.
- Regular maintenance of Flows, Apex, validation rules, and sharing settings.

## Current Limitations

- Double-booking prevention currently checks the event date rather than start and end times.
- Venue status follows the last saved event.
- Cancellation approval has a single approval step.
- Apex test classes have not yet been written.
- The project was developed in a Salesforce Developer Edition org for academic purposes and has not been deployed to production.
- Production deployment would require appropriate deployment and CI/CD processes.

## Learning Outcomes

Through this project, the team gained practical experience in:

- Salesforce CRM
- Custom object design
- Lookup and Master-Detail relationships
- Salesforce Flow
- Approval Processes
- Apex programming
- Apex Triggers
- Batch Apex
- Schedulable Apex
- Data migration
- Salesforce security
- Reports and dashboards
- Agile development

## Project Documentation

For complete implementation details, configuration steps, screenshots, test cases, architecture, and project roadmap, refer to the EventForce Management System Project Documentation.

## License

This project was developed as an academic project using Salesforce Developer Edition.

---

**EventForce Management System**  
*Centralizing event planning with Salesforce CRM.*
