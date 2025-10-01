# ServiceNow ITSM Ansible Integration

Forked from https://github.com/cloin/instruqt-snow

This project provides Ansible playbooks and inventory configurations for integrating with ServiceNow ITSM (IT Service Management) platform. It includes examples for common ServiceNow operations like incident management, configuration item creation, and automated workflows using Ansible Automation Platform.

## Overview

This repository contains automation scripts designed for educational purposes, specifically for Instruqt hands-on labs demonstrating ServiceNow and Ansible integration. The project showcases how to:

- Create and manage ServiceNow incidents programmatically
- Manage configuration items (CIs) in ServiceNow CMDB
- Collect system information and populate ServiceNow records
- Integrate ServiceNow with Ansible Automation Platform workflows

## Project Structure

```text
instruqt-snow/
├── README.md                           # This file
├── now.yml                            # ServiceNow dynamic inventory configuration
├── admin_project/                     # Administrative playbooks
│   └── create-snow-user.yml          # User account management
└── student_project/                   # Educational/demo playbooks
    ├── incident-create.yml            # Create ServiceNow incidents
    ├── change-attach.yml              # Attach files to change requests
    ├── close-records-by-user.yml      # Close records by user
    ├── collect-node-info.yml          # Gather system information
    ├── create-update-config-items.yml # Manage configuration items
    └── problem-attach.yml             # Attach files to problem records
```

## Prerequisites

- **Ansible Core**: 2.12 or higher
- **ServiceNow ITSM Collection**: `servicenow.itsm`
- **AWX Collection**: `awx.awx` (for Automation Platform integration)
- **ServiceNow Instance**: Access to a ServiceNow developer instance or sandbox
- **Environment Variables**: ServiceNow credentials configured

### Required Collections

Install the necessary Ansible collections:

```bash
ansible-galaxy collection install servicenow.itsm
ansible-galaxy collection install awx.awx
```

## Configuration

### Environment Variables

Set the following environment variables for ServiceNow authentication:

```bash
export SN_HOST=your-instance.servicenow.com
export SN_USERNAME=your_username
export SN_PASSWORD=your_password
```

### ServiceNow Dynamic Inventory

The `now.yml` file configures dynamic inventory from ServiceNow CMDB:

- Automatically groups hosts by operating system
- Filters for Linux Red Hat and Windows XP systems
- Uses the `servicenow.itsm.now` inventory plugin

## Playbook Descriptions

### Admin Project

- **`create-snow-user.yml`**: Manages ServiceNow demo user accounts through Ansible Automation Platform job templates

### Student Project

- **`incident-create.yml`**: Creates new incidents in ServiceNow with customizable descriptions and priority levels
- **`collect-node-info.yml`**: Gathers system facts (hostname, IP, MAC address, vendor) for CMDB population
- **`create-update-config-items.yml`**: Manages configuration items in ServiceNow CMDB
- **`change-attach.yml`**: Attaches files or documentation to ServiceNow change requests
- **`close-records-by-user.yml`**: Bulk closes ServiceNow records based on user criteria
- **`problem-attach.yml`**: Attaches additional information to ServiceNow problem records

## Usage Examples

### Create a ServiceNow Incident

```bash
ansible-playbook student_project/incident-create.yml
```

### Collect Node Information

```bash
ansible-playbook student_project/collect-node-info.yml -i inventory
```

### Use ServiceNow Dynamic Inventory

```bash
ansible-inventory -i now.yml --list
```

## Educational Objectives

This project demonstrates:

1. **ServiceNow API Integration**: Using Ansible modules to interact with ServiceNow REST APIs
2. **ITSM Automation**: Automating common IT service management tasks
3. **Dynamic Inventory**: Leveraging ServiceNow CMDB as an inventory source
4. **Workflow Integration**: Connecting ServiceNow with Ansible Automation Platform
5. **Data Collection**: Gathering system information for CMDB population

## Customization

### Modifying Incident Creation

Edit `student_project/incident-create.yml` to customize:

- Incident priority and impact levels
- Description templates
- Assignment groups
- Additional fields

### Extending Node Information Collection

Modify `student_project/collect-node-info.yml` to collect additional facts:

- Software inventory
- Hardware specifications
- Network configuration
- Custom application data

## Testing

Before running in production:

1. Test with a ServiceNow developer instance
2. Verify credentials and permissions
3. Review and customize variable values
4. Test individual playbooks before running workflows

## Additional Resources

- [ServiceNow ITSM Collection Documentation](https://docs.ansible.com/ansible/latest/collections/servicenow/itsm/)
- [ServiceNow Developer Portal](https://developer.servicenow.com/)
- [Ansible Automation Platform Documentation](https://docs.ansible.com/automation-controller/)

## Contributing

This project is designed for educational purposes. Feel free to:

- Add new ServiceNow integration examples
- Improve error handling
- Enhance documentation
- Submit issues for discussion
