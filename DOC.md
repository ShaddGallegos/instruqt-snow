# ServiceNow Automation with Ansible Workshop

This comprehensive workshop demonstrates how to automate ServiceNow ITSM processes using Ansible Automation Platform and the servicenow.itsm certified collection.

## Table of Contents

1. [Module 1: Creating Incidents](#module-1-creating-incidents)
   - [Introduction](#introduction)
   - [Review the Playbook](#review-the-playbook)
   - [Create Incident](#create-incident)
   - [Inspect Results](#inspect-results)
   - [Next Steps](#next-steps-1)
   - [Troubleshooting](#troubleshooting-1)

2. [Module 2: Problem Management](#module-2-problem-management)
   - [Introduction](#introduction-1)
   - [Understanding Problem-Incident Relationships](#understanding-problem-incident-relationships)
   - [Review the Playbook](#review-the-playbook-1)
   - [Attach a Problem](#attach-a-problem)
   - [Inspect Results](#inspect-results-1)
   - [Understanding the Automation](#understanding-the-automation)
   - [Next Steps](#next-steps-2)
   - [Troubleshooting](#troubleshooting-2)

3. [Module 3: Change Management](#module-3-change-management)
   - [Introduction](#introduction-2)
   - [Types of Changes](#types-of-changes)
   - [Change-Problem Relationship](#change-problem-relationship)
   - [Review the Playbook](#review-the-playbook-2)
   - [Create a Change Request](#create-a-change-request)
   - [Inspect Results](#inspect-results-2)
   - [Understanding Change Workflows](#understanding-change-workflows)
   - [Next Steps](#next-steps-3)
   - [Troubleshooting](#troubleshooting-3)

4. [Module 4: CMDB Management](#module-4-cmdb-management)
   - [Introduction](#introduction-3)
   - [Configuration Items (CIs)](#configuration-items-cis)
   - [CMDB Automation Benefits](#cmdb-automation-benefits)
   - [Lab Environment Setup](#lab-environment-setup)
   - [Review the Playbooks](#review-the-playbooks)
   - [Query Nodes and Update CMDB](#query-nodes-and-update-cmdb)
   - [Inspect Results](#inspect-results-3)
   - [Understanding CMDB Automation](#understanding-cmdb-automation)
   - [Next Steps](#next-steps-4)
   - [Troubleshooting](#troubleshooting-4)

5. [Module 5: Record Cleanup](#module-5-record-cleanup)
   - [Introduction](#introduction-4)
   - [Record Cleanup Scenarios](#record-cleanup-scenarios)
   - [Review the Cleanup Playbook](#review-the-cleanup-playbook)
   - [Query and Close Records](#query-and-close-records)
   - [Inspect Results](#inspect-results-4)
   - [Understanding Cleanup Automation](#understanding-cleanup-automation)
   - [Workshop Cleanup Complete](#workshop-cleanup-complete)
   - [Next Steps](#next-steps-5)
   - [Troubleshooting](#troubleshooting-5)

6. [Module 6: ServiceNow Inventory](#module-6-servicenow-inventory)
   - [Introduction](#introduction-5)
   - [Beyond ITSM Modules](#beyond-itsm-modules)
   - [Dynamic Inventory Benefits](#dynamic-inventory-benefits)
   - [Review Inventories](#review-inventories)
   - [Sync ServiceNow Inventory](#sync-servicenow-inventory)
   - [Inspect Results](#inspect-results-5)
   - [Inventory Use Cases](#inventory-use-cases)
   - [Advanced Configuration Options](#advanced-configuration-options)
   - [Workshop Completion](#workshop-completion)
   - [Troubleshooting](#troubleshooting-6)

---

## Module 1: Creating Incidents

Learn how to automate ServiceNow incident creation using Ansible Automation Platform and the servicenow.itsm certified collection.

### Introduction

In ITIL, an incident refers to an unplanned outage or reduction in quality of an IT service or application. ServiceNow implements technology mapped to ITIL terminology and is accepted as an industry standard for incident management.

The servicenow.itsm certified collection allows organizations to leverage incident management within Ansible Automation Platform workflows, enabling:

- Automated incident creation from monitoring systems
- Standardized incident reporting processes
- Integration with existing automation workflows
- Consistent incident data structure and classification

### Review the Playbook

A playbook has been created for incident creation: [incident-create.yml](student_project/incident-create.yml)

**Task: Inspect the playbook**

1. Open the VS Code tab in your lab environment
2. Locate and open the [incident-create.yml](student_project/incident-create.yml) file
3. Review the in-line comments to understand how the collection is being leveraged
4. Pay attention to the module parameters and their purposes

**Key elements to notice in the playbook:**

- How authentication is handled
- Required and optional parameters for incident creation
- How dynamic data is incorporated into the incident

### Create Incident

Now you'll execute the playbook through Automation Controller to create a ServiceNow incident.

**Procedure: Launch the job template**

1. Use the following login credentials to access the Automation Controller tab:
   - Username: `admin`
   - Password: `ansible123!`
2. Navigate to **Automation Execution > Templates**
3. Locate the **1 - Create incident (incident-create.yml)** job template
4. Click the rocket icon to launch the job

Monitor the job execution and note:
- The job status and any output messages
- The incident number created (you'll need this for verification)
- Any error messages or warnings

### Inspect Results

Verify that the incident was successfully created in ServiceNow.

**ServiceNow Login Credentials:**
- Username: `aap-roadshow`
- Password: `Ans1ble123!`

**Procedure: Verify incident creation**

1. Use the ServiceNow credentials from your lab environment to access the ServiceNow tab
2. In ServiceNow, select **incidents**
3. Locate your newly created incident in the list
4. Click on the incident to view its details

**Verification Points**

To confirm the incident was created by your automation:

- **Username**: Your unique lab username should appear in the incident description
- **Incident Number**: Should match the number displayed in the Automation Controller job output
- **Timestamp**: Should correspond to when you ran the job
- **Status**: Should be in "New" or "Active" state

**Expected Results**

You should see a new incident with:
- A unique incident number (e.g., INC0012345)
- Your username in the description
- Appropriate priority and category settings
- Timestamp matching your job execution

### Next Steps

Once you've successfully created and verified your incident, you're ready to move on to Module 2, where you'll learn about problem management and how to attach problems to existing incidents.

### Troubleshooting

If you encounter issues:

1. **Job fails to execute**: Check your Automation Controller credentials and network connectivity
2. **Incident not visible**: Verify you're logged into ServiceNow with the correct credentials
3. **Permission errors**: Ensure your ServiceNow user has appropriate ITSM permissions

For additional support, refer to the lab environment documentation or contact your instructor.

---

## Module 2: Problem Management

Learn how to automate ServiceNow problem management by creating problems and linking them to existing incidents.

### Introduction

In ServiceNow's ITIL implementation, a problem represents the underlying cause of one or more incidents. Problems are used to:

- Identify root causes of recurring incidents
- Prevent future incidents through permanent fixes
- Track workarounds and known errors
- Maintain relationships between incidents and their underlying causes

The root cause of a problem may not be known at creation time and often requires investigation through the problem management process.

### Understanding Problem-Incident Relationships

Problems and incidents have a many-to-one relationship:

- One problem can be associated with multiple incidents
- Each incident can be linked to at most one problem
- Problems help identify patterns and systemic issues

### Review the Playbook

A new playbook called [problem-attach.yml](student_project/problem-attach.yml) has been added to your workspace.

**Task: Inspect the problem creation playbook**

1. Open the VS Code tab in your lab environment
2. Locate and open the [problem-attach.yml](student_project/problem-attach.yml) file
3. Review the playbook structure and logic
4. Pay attention to how it queries for existing incidents

**Key aspects to notice:**

- The playbook first queries for existing incident numbers you created
- It uses the returned incident data in the problem creation task
- The problem is automatically linked to the incident
- Additional problem-specific fields are populated

### Attach a Problem

Execute the playbook to create a problem and associate it with your existing incident.

**Procedure: Launch the problem attachment job**

1. Navigate to the Automation Controller tab
2. Go to **Automation Execution > Templates**
3. Locate the **2 - Attach problem (problem-attach.yml)** job template
4. Click the rocket icon to execute the job

**What Happens During Execution**

The playbook performs these operations:

1. **Query Phase**: Searches for incidents created by your user account
2. **Problem Creation**: Creates a new problem record in ServiceNow
3. **Relationship Establishment**: Links the problem to the identified incident
4. **Field Population**: Sets appropriate problem details and categorization

Monitor the job output to see:
- Which incident was found and selected
- The problem number that was created
- The relationship establishment between records

### Inspect Results

Verify that the problem was created and properly linked to your incident.

**Verify Problem Creation**

**Procedure: Check the new problem**

1. Access the ServiceNow tab using your credentials
2. Select the "Favorites" tab and select "Problem - assigned to me"
3. Select the appropriate problems view
4. Locate your newly created problem

Look for:
- A new problem number (e.g., PRB0012345)
- Your username in the problem description or assignment
- Proper categorization and priority settings
- Timestamp matching your job execution

**Verify Incident Update**

**Procedure: Check incident-problem relationship**

1. In ServiceNow, navigate to **Self-service - Incidents**
2. Select your incident from Module 1
3. Review the incident details for problem references
4. Confirm the problem number appears in the related records

The incident should now show:
- Updated status (if applicable)
- Reference to the associated problem number
- Modified timestamp reflecting the relationship update

**Expected Relationship**

| Field | Expected Value |
|-------|----------------|
| Incident Status | May be updated to "In Progress" or similar |
| Problem Reference | Should display the new problem number |
| Last Modified | Should reflect the time of problem attachment |
| Related Records | Problem should appear in related lists |

### Understanding the Automation

This module demonstrates several important automation concepts:

- **Data Querying**: How to search for existing records using Ansible
- **Dynamic Relationships**: Creating links between different record types
- **Workflow Integration**: Building upon previous automation steps
- **ITIL Process Automation**: Implementing standard ITSM workflows

### Next Steps

With your problem successfully created and linked, you're ready to proceed to Module 3, where you'll learn about change management and how to create change requests for resolving problems.

### Troubleshooting

Common issues and solutions:

- **No incidents found**: Ensure you completed Module 1 successfully
- **Permission errors**: Verify your ServiceNow user has problem management permissions
- **Relationship not visible**: Check if you're viewing the correct incident record
- **Job execution fails**: Review the playbook syntax and authentication settings

For additional assistance, consult your lab environment documentation.

---

## Module 3: Change Management

Learn how to automate ServiceNow change management by creating change requests to address problems and incidents.

### Introduction

In ITIL, a change request represents any addition, modification, or removal made to address problems or improve IT services. ServiceNow change management enables organizations to:

- Control and track all changes to IT infrastructure
- Minimize risk through proper planning and approval processes
- Maintain change records for audit and compliance purposes
- Coordinate changes with business requirements and schedules

### Types of Changes

ServiceNow typically categorizes changes into several types:

- **Standard Changes**: Pre-approved, low-risk changes that follow established procedures
- **Normal Changes**: Regular changes that require approval through the Change Advisory Board (CAB)
- **Emergency Changes**: Urgent changes needed to resolve critical issues

### Change-Problem Relationship

Changes are often created to:

- Resolve known problems permanently
- Implement workarounds for ongoing issues
- Address root causes identified during problem investigation
- Prevent recurrence of incidents

### Review the Playbook

A new playbook called [change-attach.yml](student_project/change-attach.yml) has been created in your workspace.

**Task: Inspect the change request playbook**

1. Open the VS Code tab in your lab environment
2. Locate and open the [change-attach.yml](student_project/change-attach.yml) file
3. Review the playbook structure and parameters
4. Note how it references existing problems or incidents

**Key elements to observe:**

- Change request categorization and priority
- Required approval workflows
- Risk assessment and impact analysis
- Implementation timeline and rollback plans

### Create a Change Request

Execute the playbook to create a change request that addresses your problem from Module 2.

**Procedure: Launch the change request job**

1. Navigate to the Automation Controller tab
2. Go to **Automation Execution > Templates**
3. Locate the **3 - Attach change request (change-attach.yml)** job template
4. Click the rocket icon to launch the job
5. Monitor the job execution for completion

**Change Request Details**

The playbook will create a change request with:

- **Title**: "Reboot the webserver" (example remediation action)
- **Description**: Detailed explanation of the proposed change
- **Justification**: Reference to the related problem or incident
- **Risk Assessment**: Evaluation of potential impact
- **Implementation Plan**: Steps to execute the change

Monitor the job output for:
- Change request number assignment
- Status and state information
- Any validation or error messages

### Inspect Results

Verify that the change request was successfully created and properly configured.

**Procedure: Verify change request creation**

1. Access the ServiceNow tab using your credentials
2. Navigate to your pre-configured favorites
3. Select **Change - Open** to view open change requests
4. Locate your newly created change request

**Expected Change Request Properties**

Look for these key attributes in your change request:

| Field | Expected Value |
|-------|----------------|
| Short Description | "Reboot the webserver" or similar remediation action |
| State | "New" or "Assess" depending on configuration |
| Priority | Appropriate based on related problem/incident |
| Category | Software or Hardware as applicable |
| Description | Detailed explanation of the change purpose |
| Justification | Reference to related problem or incident |

**Additional Field Validation**

Verify that other relevant fields have been populated:

- **On Hold Reason**: May be set if approval is pending
- **Assigned To**: Should reflect the appropriate change implementer
- **Planned Start/End Dates**: Timeline for change implementation
- **Risk**: Assessment of potential impact (Low, Medium, High)

### Understanding Change Workflows

This module demonstrates several change management concepts:

- **Automated Change Creation**: Programmatic generation of change requests
- **Problem-Change Linkage**: Connecting changes to their underlying justification
- **Standardized Documentation**: Consistent change request formatting
- **Integration Points**: How changes fit into overall ITSM processes

**Change Approval Process**

In a production environment, your change request would typically:

1. **Assessment**: Technical review of proposed change
2. **Authorization**: Approval by Change Advisory Board (CAB)
3. **Scheduling**: Coordination with business requirements
4. **Implementation**: Execution of the approved change
5. **Review**: Post-implementation validation and closure

### Next Steps

With your change request successfully created, you're ready to proceed to Module 4, where you'll learn about CMDB management and how to query and update configuration items that might be affected by your changes.

### Troubleshooting

Common issues and solutions:

- **Change not created**: Verify ServiceNow user has change management permissions
- **Missing related records**: Ensure previous modules completed successfully
- **Approval workflow issues**: Check change management configuration settings
- **Field validation errors**: Review required vs. optional field settings

For additional support, refer to your lab environment documentation or contact your instructor.

---

## Module 4: CMDB Management

Learn how to automate ServiceNow Configuration Management Database (CMDB) operations using Ansible to query and update configuration items.

### Introduction

In ITIL, a Configuration Management Database (CMDB) is a centralized repository that organizations use to track hardware and software assets throughout their lifecycle. The ServiceNow CMDB serves as the single source of truth for IT asset management, providing:

- **Asset Tracking**: Complete inventory of IT infrastructure components
- **Relationship Mapping**: Dependencies and connections between configuration items
- **Change Impact Analysis**: Understanding how changes affect related systems
- **Service Mapping**: Linking business services to underlying infrastructure

### Configuration Items (CIs)

Configuration Items represent individual components in your IT infrastructure:

- **Hardware**: Servers, network devices, storage systems
- **Software**: Applications, operating systems, databases
- **Services**: Business services, technical services
- **Documentation**: Procedures, policies, service level agreements

### CMDB Automation Benefits

Using Ansible to automate CMDB operations provides:

- **Accuracy**: Automated data collection reduces manual entry errors
- **Consistency**: Standardized data formats and update procedures
- **Timeliness**: Real-time updates as infrastructure changes
- **Integration**: Seamless connection with existing automation workflows

### Lab Environment Setup

For this module, two Red Hat Enterprise Linux (RHEL) servers have been automatically provisioned:

- **node1**: Primary test server
- **node2**: Secondary test server

These servers have been added to the Automation Controller inventory and are ready for CMDB integration.

### Review the Playbooks

Two specialized playbooks have been created in your workspace:

- [collect-node-info.yml](student_project/collect-node-info.yml): Gathers detailed information about the RHEL nodes
- [create-update-config-items.yml](student_project/create-update-config-items.yml): Creates or updates configuration items in the CMDB

**Task: Examine the CMDB playbooks**

1. Open the VS Code tab in your lab environment
2. Review [collect-node-info.yml](student_project/collect-node-info.yml) to understand data collection methods
3. Examine [create-update-config-items.yml](student_project/create-update-config-items.yml) to see how CI updates work
4. Note the data mapping between Ansible facts and ServiceNow fields

**Current CMDB State**

Before running the automation, examine the current state of Linux configuration items:

**Procedure: View existing Linux CIs**

1. Access the ServiceNow tab
2. In the filter navigator, type "Linux"
3. Navigate to **Configuration → Servers → Linux**
4. Review the current list of Linux server configuration items

Note the current number of Linux servers and their details - you'll compare this after running the automation.

### Query Nodes and Update CMDB

Execute the workflow to collect node information and update the ServiceNow CMDB with configuration items.

**Workflow Job Template**

The CMDB automation has been implemented as a Workflow Job Template that combines multiple operations:

**Procedure: Execute the CMDB workflow**

1. Navigate to the Automation Controller tab
2. Go to **Automation Execution → Templates**
3. Locate the **4.0 - Query node info and update CMDB (multiple job templates)** workflow
4. Click the rocket icon to launch the workflow

**Workflow Visualization**

The Workflow Job Template includes a visualization feature:

- **Workflow Map**: Visual representation of job dependencies and flow
- **Real-time Status**: Live updates showing job progress
- **Interactive Nodes**: Click on workflow nodes to view individual job details
- **Parallel Execution**: Multiple jobs running simultaneously for efficiency

**Task: Monitor workflow execution**

1. After launching the workflow, look for the visualization button
2. Click the visualization icon to open the workflow map
3. Observe the job nodes and their execution status
4. Click on individual nodes to view job details and output
5. Monitor the overall workflow progress

**Workflow Components**

The workflow typically includes these phases:

1. **Discovery Phase**: Collect system information from target nodes
2. **Data Processing**: Transform collected data into ServiceNow format
3. **CMDB Update**: Create or update configuration items
4. **Relationship Mapping**: Establish connections between CIs
5. **Validation**: Verify successful CMDB updates

### Inspect Results

Verify that the configuration items were successfully created or updated in the ServiceNow CMDB.

**Verify CMDB Updates**

**Procedure: Check updated Linux configuration items**

1. Return to the ServiceNow tab
2. In the filter navigator, type "Linux"
3. Navigate to **Configuration → Servers → Linux**
4. Review the updated list of Linux server configuration items
5. Compare with the initial state you observed earlier

**Expected Results**

You should observe the following changes:

- **New Configuration Items**: Two new Linux server CIs (node1 and node2)
- **IP Address Population**: Network information automatically populated
- **System Details**: Hardware and software specifications included
- **Timestamps**: Creation or update times reflecting the automation execution

**Configuration Item Details**

Click on each new configuration item to examine the populated fields:

| Field Category | Expected Information |
|----------------|---------------------|
| Basic Information | Hostname, FQDN, operating system |
| Network Details | IP addresses, MAC addresses, network interfaces |
| Hardware Specs | CPU count, memory, disk space |
| Software Info | Operating system version, installed packages |
| Discovery Data | Last discovered date, discovery source |

**Data Accuracy Validation**

Verify that the automated data collection captured accurate information:

- **IP Addresses**: Should match the actual node network configuration
- **System Specifications**: CPU, memory, and disk information should be current
- **OS Details**: Operating system version and architecture should be correct
- **Hostnames**: Should correspond to the actual server names (node1, node2)

### Understanding CMDB Automation

This module demonstrates several key concepts:

- **Automated Discovery**: How Ansible can collect system information
- **Data Transformation**: Converting system facts to ServiceNow format
- **CMDB Integration**: Programmatic creation and updating of CIs
- **Workflow Orchestration**: Coordinating multiple automation tasks

**Benefits Realized**

- **Reduced Manual Effort**: Eliminates manual data entry for new systems
- **Improved Accuracy**: Automated collection reduces human errors
- **Consistent Updates**: Standardized data format and update procedures
- **Real-time Synchronization**: CMDB stays current with infrastructure changes

### Next Steps

With your CMDB successfully updated with new configuration items, you're ready to proceed to Module 5, where you'll learn about automated record cleanup and maintenance tasks.

### Troubleshooting

Common issues and solutions:

- **CIs not created**: Verify node connectivity and ServiceNow permissions
- **Missing IP addresses**: Check network configuration and discovery settings
- **Duplicate entries**: Review CI identification and matching logic
- **Permission errors**: Ensure ServiceNow user has CMDB write permissions
- **Workflow failures**: Check individual job logs for specific error messages

For additional assistance, consult your lab environment documentation or contact your instructor.

---

## Module 5: Record Cleanup

Learn how to automate ServiceNow record maintenance and cleanup tasks using Ansible to query and close records systematically.

### Introduction

As part of good ITSM hygiene, it's important to maintain clean and current records in ServiceNow. This module demonstrates how to automate the cleanup of records created during the workshop, showcasing techniques that can be applied to regular maintenance tasks in production environments.

### Record Cleanup Scenarios

Automated record cleanup is useful for:

- **Workshop/Training Cleanup**: Removing test data after learning exercises
- **Periodic Maintenance**: Closing stale or abandoned records
- **Data Governance**: Ensuring records follow proper lifecycle management
- **Compliance**: Meeting retention and cleanup requirements

**Cleanup Strategy**

The cleanup process involves several steps:

1. **Discovery**: Query for records matching specific criteria
2. **Validation**: Ensure records are appropriate for cleanup
3. **Processing**: Update or close records systematically
4. **Verification**: Confirm cleanup operations completed successfully

### Review the Cleanup Playbook

A specialized playbook called [close-records-by-user.yml](student_project/close-records-by-user.yml) has been created for this cleanup operation.

**Task: Examine the cleanup playbook**

1. Open the VS Code tab in your lab environment
2. Locate and open the [close-records-by-user.yml](student_project/close-records-by-user.yml) file
3. Review the playbook structure and logic
4. Pay attention to the different module types used

**Understanding Info Modules**

The playbook uses several `*_info` modules that provide query capabilities:

- `servicenow.itsm.incident_info`: Queries incident records
- `servicenow.itsm.problem_info`: Searches problem records
- `servicenow.itsm.change_request_info`: Finds change request records

These modules search for active records created by your username and return structured data for processing.

**Data Transformation Process**

The playbook demonstrates advanced Ansible techniques:

1. **Query Execution**: Info modules retrieve relevant records
2. **Data Processing**: Ansible transforms returned data into manageable lists
3. **Record Updates**: Lists are passed to update modules for bulk processing
4. **Field Handling**: Uses the `other` parameter for custom or non-standard fields

**The 'other' Parameter**

For fields not directly implemented by ServiceNow modules, the `other` parameter allows specification of:

- Custom fields specific to your ServiceNow instance
- Additional standard fields not covered by module parameters
- Complex field values requiring special formatting

### Query and Close Records

Execute the cleanup automation to systematically close all records created during the workshop.

**Cleanup Execution**

**Procedure: Launch the cleanup job**

1. Navigate to the Automation Controller tab
2. Go to **Automation Execution → Templates**
3. Locate the **5 - Query and close records by user (close-records-by-user.yml)** job template
4. Click the rocket icon to launch the cleanup job
5. Monitor the job output carefully during execution

**Monitoring the Cleanup Process**

As the job runs, observe the following phases:

1. **Discovery Phase**: Queries identify records for cleanup
   - Incident records matching your username
   - Problem records created by you
   - Change requests under your name

2. **Validation Phase**: Confirms records are appropriate for closure
   - Verifies record ownership
   - Checks current status eligibility
   - Validates business rules compliance

3. **Processing Phase**: Updates and closes identified records
   - Updates incident status to "Resolved" or "Closed"
   - Closes problem records with appropriate resolution
   - Completes change requests with implementation status

4. **Reporting Phase**: Provides summary of cleanup actions
   - Lists all affected record numbers
   - Reports success/failure status
   - Documents any errors or exceptions

**Expected Job Output**

The job output should display:

- Number of records found for each type (incidents, problems, changes)
- Specific record numbers being processed
- Status updates for each closure operation
- Final summary of completed actions

### Inspect Results

Verify that all workshop records have been successfully closed or removed from active status.

**Verification Process**

**Procedure: Confirm cleanup completion**

1. Wait for the cleanup job to complete successfully
2. Review the job output for the summary of actions taken
3. Note all record numbers that were processed
4. Access the ServiceNow tab to verify the changes

**ServiceNow Verification**

Check each record type to confirm cleanup:

**Incidents**

1. Navigate to **Self-service - Incidents** in ServiceNow
2. Look for incidents created during the workshop
3. Verify they now show "Resolved" or "Closed" status
4. Check that closure notes indicate automated cleanup

**Problems**

1. Access the **Problems** view in ServiceNow
2. Search for problems created during Modules 2-3
3. Confirm they show appropriate closed status
4. Verify resolution details are populated

**Change Requests**

1. Go to **Change - Open** or **Change - All** views
2. Locate change requests from Module 3
3. Verify they show completed or closed status
4. Check implementation and closure details

**Expected Cleanup Results**

After successful cleanup, you should observe:

| Record Type | Expected State |
|-------------|----------------|
| Incidents | Status: Resolved/Closed, Resolution: Automated cleanup |
| Problems | State: Closed, Resolution: Workshop completion |
| Change Requests | State: Closed/Complete, Implementation: Automated |
| Configuration Items | Remain active (CIs typically aren't "closed") |

**Refresh Views**

Some ServiceNow views may cache data:

- Refresh your browser or press F5
- Navigate away from and back to list views
- Use the "Refresh" button in ServiceNow if available
- Check timestamps to ensure you're seeing current data

### Understanding Cleanup Automation

This module demonstrates several important concepts:

**Bulk Operations**

- **Efficient Processing**: Handle multiple records in a single operation
- **Consistent Updates**: Apply standardized closure procedures
- **Error Handling**: Manage individual record failures gracefully
- **Audit Trail**: Maintain complete records of automated actions

**Production Applications**

Similar techniques can be used for:

- **Scheduled Maintenance**: Regular cleanup of old or stale records
- **Data Lifecycle Management**: Implementing retention policies
- **Compliance Automation**: Meeting regulatory cleanup requirements
- **Environment Management**: Sanitizing test/development instances

**Best Practices Demonstrated**

- **Query Filtering**: Target specific records based on criteria
- **Data Validation**: Confirm records before making changes
- **Incremental Processing**: Handle records systematically
- **Result Verification**: Confirm successful completion

### Workshop Cleanup Complete

With all workshop records properly closed and cleaned up, your ServiceNow instance is ready for the final module. The cleanup process demonstrates how automation can maintain data hygiene and implement consistent record lifecycle management.

### Next Steps

You're now ready to proceed to Module 6, the final module of this workshop, where you'll explore how to use ServiceNow as a dynamic inventory source for Ansible operations.

### Troubleshooting

Common cleanup issues and solutions:

- **Records not found**: Verify previous modules completed successfully
- **Permission errors**: Ensure ServiceNow user has update/close permissions
- **Partial cleanup**: Check for records in different states or assignments
- **Job failures**: Review individual record processing for specific errors
- **Validation errors**: Confirm business rules allow automated closure

For additional support, refer to your lab environment documentation or contact your instructor.

---

## Module 6: ServiceNow Inventory

Learn how to use ServiceNow CMDB as a dynamic inventory source for Ansible Automation Platform operations.

### Introduction

Throughout this workshop, you've explored various modules from the servicenow.itsm collection for automating incident management processes. While the examples demonstrated basic automation scenarios, these modules are highly flexible and can be adapted to numerous production use cases within ITSM.

### Beyond ITSM Modules

The servicenow.itsm collection provides more than just ITSM task automation. One of its most powerful features is the dynamic inventory plugin that allows you to query endpoints directly from the ServiceNow CMDB.

### Dynamic Inventory Benefits

Using ServiceNow as an Ansible inventory source provides:

- **Single Source of Truth**: Eliminate duplicate inventory management
- **Real-time Data**: Inventory updates automatically as CMDB changes
- **Rich Metadata**: Leverage all CMDB attributes for targeting and grouping
- **Compliance**: Ensure automation only targets authorized systems
- **Integration**: Seamless connection between ITSM and automation workflows

**Inventory Architecture**

The ServiceNow inventory plugin:

1. **Queries CMDB**: Retrieves configuration items based on filters
2. **Transforms Data**: Converts CI data into Ansible inventory format
3. **Creates Groups**: Organizes hosts by attributes (OS, manufacturer, location)
4. **Provides Variables**: Makes CMDB fields available as host variables
5. **Updates Dynamically**: Refreshes inventory data on demand

**Current State**

A new ServiceNow inventory has been pre-configured in Automation Controller, but it hasn't synchronized with the CMDB yet. You'll explore this inventory and trigger its first synchronization.

### Review Inventories

Examine the current state of inventories in Automation Controller and understand the ServiceNow integration architecture.

**Current Host Inventory**

**Procedure: Check existing hosts**

1. Open the Automation Controller tab
2. Navigate to **Hosts** in the left navigation pane
3. Observe the current host list

**Expected Observation**

The host list appears empty or contains only the lab infrastructure hosts. This is expected because:

- The ServiceNow inventory hasn't been synchronized yet
- The integration works API-to-API, not through individual host connections
- Hosts will appear after ServiceNow CMDB synchronization

**Understanding the Integration**

The Ansible-ServiceNow integration architecture:

- **API Integration**: Direct communication between Automation Controller and ServiceNow APIs
- **No Agent Required**: Target systems don't need Ansible agents or SSH access
- **CMDB as Source**: ServiceNow CMDB serves as the authoritative inventory source
- **Dynamic Updates**: Inventory refreshes based on current CMDB state

### Sync ServiceNow Inventory

Trigger the ServiceNow inventory synchronization to populate Automation Controller with CMDB data.

**Inventory Synchronization Process**

**Procedure: Initiate inventory sync**

1. In Automation Controller, navigate to **Inventories** in the left navigation
2. Locate and click on the **ServiceNow inventory**
3. Select the **Sources** tab within the inventory details
4. Click the **Sync** button to initiate synchronization

**What Happens During Sync**

The synchronization process triggers multiple operations:

1. **API Query**: Automation Controller queries ServiceNow CMDB using configured filters
2. **Data Retrieval**: ServiceNow returns configuration items matching the criteria
3. **Data Processing**: Raw CMDB data is transformed into Ansible inventory format
4. **Group Creation**: Hosts are organized into groups based on attributes
5. **Variable Assignment**: CMDB fields become available as host variables

**Monitoring Sync Progress**

**Procedure: Track synchronization jobs**

1. Navigate to **Jobs** in the left navigation pane
2. Look for inventory sync jobs that were triggered
3. Monitor job progress and status
4. Review job output for any errors or warnings

The sync process may take a few minutes depending on:

- Number of configuration items in the CMDB
- Complexity of the inventory query
- Network latency between systems
- ServiceNow instance performance

### Inspect Results

Examine the synchronized inventory data and understand how ServiceNow CMDB information appears in Automation Controller.

**Verify Host Population**

**Procedure: Check synchronized hosts**

1. Once the sync jobs complete, navigate to **Hosts** in the left navigation
2. Observe the hosts that have been pulled from the ServiceNow CMDB
3. Note the host names, groups, and associated metadata

**Procedure: Explore inventory details**

1. Go to **Inventories → ServiceNow inventory → Hosts**
2. Review the imported hosts and their properties
3. Examine the group memberships and organization
4. Click on individual hosts to see their variables and metadata

**Understanding Inventory Configuration**

The ServiceNow inventory uses a specific configuration that demonstrates flexible querying:

```yaml
# Group hosts automatically, according to values of manufacturer and os columns.
# Include only records with the specified operating systems.
# Groups will most likely overlap.
plugin: servicenow.itsm.now
group_by:
  manufacturer:
  os:
    includes:
      - Linux Red Hat
      - Windows XP
```

**Configuration Breakdown**

- **Plugin**: Uses `servicenow.itsm.now` for CMDB integration
- **Filtering**: Only includes specified operating systems (Linux Red Hat, Windows XP)
- **Grouping**: Creates groups based on manufacturer and operating system
- **Overlapping Groups**: Hosts may belong to multiple groups simultaneously

**Expected Groups**

The inventory configuration should create groups such as:

- **By Operating System**: `os_linux_red_hat`, `os_windows_xp`
- **By Manufacturer**: Groups based on hardware manufacturers
- **Combined Criteria**: Intersection of OS and manufacturer attributes

**Host Variables**

Each host imported from ServiceNow includes variables derived from CMDB fields:

- System specifications (CPU, memory, disk)
- Network configuration (IP addresses, MAC addresses)
- Software inventory (installed applications, patch levels)
- Administrative data (asset tags, locations, owners)

### Inventory Use Cases

This dynamic inventory enables powerful automation scenarios:

**Targeted Automation**

- **OS-Specific Tasks**: Run playbooks only on specific operating systems
- **Hardware-Based Operations**: Target actions based on manufacturer or model
- **Location-Aware Automation**: Execute tasks based on physical or logical location
- **Role-Based Targeting**: Use business application assignments for targeting

**Integration Benefits**

- **Compliance**: Ensure automation only affects authorized systems
- **Accuracy**: Inventory always reflects current CMDB state
- **Efficiency**: Eliminate manual inventory maintenance
- **Auditability**: Maintain clear relationship between ITSM and automation

### Advanced Configuration Options

The ServiceNow inventory plugin supports numerous configuration options:

- **Custom Queries**: Filter CIs using any CMDB field
- **Field Mapping**: Map ServiceNow fields to Ansible variables
- **Group Creation**: Define complex grouping strategies
- **Caching**: Control inventory refresh frequency
- **Authentication**: Various ServiceNow authentication methods

### Workshop Completion

**Congratulations!**

You have successfully completed the ServiceNow Automation with Ansible workshop! Throughout this journey, you've learned to:

1. Create and manage ServiceNow incidents through automation
2. Implement automated problem management workflows
3. Automate change request creation and tracking
4. Query and update ServiceNow CMDB configuration items
5. Perform automated record cleanup and maintenance
6. Use ServiceNow CMDB as a dynamic Ansible inventory source

**Key Takeaways**

- **Integration Power**: Ansible and ServiceNow provide seamless ITSM automation
- **Workflow Automation**: Complex ITIL processes can be fully automated
- **Data Synchronization**: Maintain consistency between systems automatically
- **Operational Efficiency**: Reduce manual tasks and improve accuracy
- **Scalability**: Automation scales to handle enterprise-level operations

**Next Steps**

To continue your ServiceNow automation journey:

- Explore additional modules in the servicenow.itsm collection
- Implement custom workflows for your organization's needs
- Integrate ServiceNow automation with monitoring and alerting systems
- Develop custom inventory configurations for your environment
- Create reusable automation patterns and best practices

### Troubleshooting

Common inventory issues and solutions:

- **No hosts imported**: Check ServiceNow connectivity and query filters
- **Missing groups**: Verify group_by configuration and CMDB data
- **Authentication errors**: Confirm ServiceNow credentials and permissions
- **Sync job failures**: Review ServiceNow API limits and instance performance
- **Outdated data**: Trigger manual sync or adjust cache settings

For additional support, refer to the ServiceNow and Ansible documentation or contact your system administrators.