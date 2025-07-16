# Ansible Roles for Splunk Cloud – Overview and Details

This document summarizes the new and relevant Ansible roles added to this project for robust, idempotent management of Splunk Cloud resources.

---

## New Ansible Roles

### 1. `splunk_cloud_hec_token`
**Purpose:**  
Manages HTTP Event Collector (HEC) tokens in Splunk Cloud via the ACS API.

**Key Features:**
- **Idempotent management**: Ensures HEC tokens are only created if they do not exist, and only updated if their configuration differs from the desired state.
- **Field-by-field comparison**: Updates are only sent if there are actual differences between local and remote token configurations.
- **Index validation**: Validates that all `allowedIndexes` referenced in a HEC token exist in Splunk Cloud before attempting to create or update the token.
- **Pagination support**: Handles paginated API responses for both HEC tokens and indexes, aggregating results as needed.
- **Error handling**: Fails early and clearly if invalid indexes are referenced or if API errors occur.
- **Minimal API payloads**: Only sends relevant fields to the API, avoiding Ansible-specific keys.

---

### 2. `splunk_cloud_index`
**Purpose:**  
Manages Splunk Cloud indexes via the ACS API.

**Key Features:**
- **Idempotent management**: Ensures indexes are created, updated, or deleted as needed to match the desired state.
- **Pagination support**: Handles paginated index listings from the API.
- **Field-by-field comparison**: Only updates indexes if their configuration differs from the desired state.
- **Error handling**: Provides clear feedback on API errors or misconfigurations.

---

### 3. `splunk_cloud_user`
**Purpose:**  
Manages Splunk Cloud users via the ACS API.

**Key Features:**
- **Idempotent management**: Ensures users are created, updated, or deleted as needed.
- **Strong password generation**: Generates strong, 10-digit passwords for new users and outputs them at creation time.
- **Header management**: Handles required API headers (e.g., `Federated-Search-Manage-Ack`) for user updates.
- **Field-by-field comparison**: Only updates users if their configuration differs from the desired state.

---

### 4. `splunk_cloud_role`
**Purpose:**  
Manages Splunk Cloud roles via the ACS API.

**Key Features:**
- **Idempotent management**: Ensures roles are created, updated, or deleted as needed.
- **Field-by-field comparison**: Only updates roles if their configuration differs from the desired state.
- **Error handling**: Provides clear feedback on API errors or misconfigurations.

> **Note:**  
The `splunk_cloud_index`, `splunk_cloud_user`, and `splunk_cloud_role` roles were referenced as existing or recently improved, but the main new addition in this development cycle was the `splunk_cloud_hec_token` role, which follows the same robust, idempotent, and API-driven design as the others.

---

## Additional Roles

### `splunk_cloud_maintenance_window`
**Purpose:**  
Manages maintenance windows and change freeze requests in Splunk Cloud Platform.

**Key Features:**
- Retrieves current maintenance window preferences and schedules from Splunk Cloud.
- Processes and applies customer-initiated change freeze requests (e.g., blackout periods for changes).
- Converts inventory-defined freeze requests into the API format and updates preferences via the Splunk Cloud API.
- Ensures idempotency by only updating preferences if there are actual changes.

---

### `splunk_cloud_limits_conf`
**Purpose:**  
Manages `limits.conf` configurations in Splunk Cloud Platform.

**Key Features:**
- Allows declarative management of Splunk’s `limits.conf` settings (which control various operational limits in Splunk).
- Ensures that configuration changes are applied in an idempotent and automated way via the Splunk Cloud API.
- Useful for tuning and compliance with operational best practices.

---

### `splunk_cloud_ddss_storage`
**Purpose:**  
Manages DDSS (Dynamic Data Self Storage) locations in Splunk Cloud Platform.

**Key Features:**
- Allows you to define and manage self storage bucket locations for indexes in Splunk Cloud.
- Ensures that storage configuration is consistent and managed as code.
- Supports idempotent updates and clear feedback on configuration changes.

---

## Summary Table

| Role Name                        | Purpose/Functionality                                                                 |
|-----------------------------------|--------------------------------------------------------------------------------------|
| `splunk_cloud_hec_token`          | Manage HEC tokens in Splunk Cloud                                                    |
| `splunk_cloud_index`              | Manage indexes in Splunk Cloud                                                       |
| `splunk_cloud_user`               | Manage users in Splunk Cloud                                                         |
| `splunk_cloud_role`               | Manage roles in Splunk Cloud                                                         |
| `splunk_cloud_maintenance_window` | Manage maintenance windows and change freeze requests in Splunk Cloud                |
| `splunk_cloud_limits_conf`        | Manage `limits.conf` configuration in Splunk Cloud                                   |
| `splunk_cloud_ddss_storage`       | Manage DDSS self storage locations for Splunk Cloud indexes                          |

---

If you need more detail or usage examples for any of these roles, please refer to the role documentation or ask for examples. 