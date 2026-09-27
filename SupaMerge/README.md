# Product URL

https://apps-gallery.dev/Apps/supa-merge

# Purpose

Duplicate records split customer information across your system. Sales teams can contact the same person twice, service teams can miss relevant details, and reporting can count the same customer more than once. Cleaning up those records takes more than deleting a row: someone needs to decide which information is correct and what happens to the related records.

Dynamics 365 and Dataverse already provide duplicate detection, cross-table matching, background detection jobs, and merging for selected standard tables. The gap appears when your business needs to merge custom-table records, express more complex matching logic, or apply its own rules for which values survive. Out-of-the-box detection combines conditions within a rule using AND and allows only five published rules per table. Native merging does not support custom tables, and its standard field-selection options do not provide a configurable business-rule script.

**Supa Merge closes those gaps with custom-table merging, nested AND/OR matching, more than five active detection rules per table, and scripted Auto Merge field selection.** Unlike out-of-the-box merge, it also lets administrators use a custom Dataverse view to control which fields appear in the merge window and their order, helping users focus on the information that matters. It can reactivate an inactive record chosen as the survivor before merging, removing a separate preparation step required by the standard merge experience.

For business teams, this means duplicate cleanup can cover the custom records their processes depend on. For consultants and architects, it provides configurable capabilities that would otherwise require additional development around the standard tools. Users still review matches and control merges within their model-driven app, supporting cleaner reporting and more complete records.

# Key Features

## Supa Merge vs. Out-of-the-Box Dynamics 365 and Dataverse

The comparison below covers Microsoft's standard duplicate detection and merge capabilities, without bespoke extensions. Supa Merge capabilities require the relevant configuration and supported tables.

| Capability | Out of the box | Supa Merge |
| --- | --- | --- |
| **Merge custom-table records** | Native merge supports Account, Contact, Lead, and Case—not custom tables. | Extends merging to supported custom tables, including eligible related-record reparenting and a link from the deactivated duplicate to the survivor. |
| **Control merge-window fields with a custom view** | Does not let administrators assign a custom Dataverse view to control the fields displayed in the merge window. | Uses a configured custom Dataverse view to determine which fields appear and in what order, tailoring the comparison to each table's business needs. |
| **Combine alternative matching conditions in one rule** | Conditions within a rule use AND. Alternative strategies require separate rules; there is no nested AND/OR rule builder. | Supports nested FetchXML AND/OR filters—for example, matching email **OR** matching both name **AND** phone in one rule. |
| **Use more than five active rules per table** | A maximum of five duplicate detection rules can be published per table at one time. | Its separate rule engine has no five-rule cap. Rules can be activated independently, subject to processing limits. |
| **Apply business-specific field-selection logic** | Provides manual selection and built-in options such as choosing populated fields. The standard dialog has no configurable script for deciding which values win. | An administrator-authored JavaScript script selects fields to copy when a user invokes Auto Merge on a saved pair. |
| **Keep an inactive record as the survivor** | The standard merge experience cannot merge into an inactive record; it must be reactivated first. | Reactivates the chosen survivor before merging, using table metadata or configured status and status-reason values, subject to valid transitions and permissions. |
| Detect matches across different tables | Supported through base and matching record types, including eligible custom tables. | Also supported through configured rules. Neither solution merges records across different tables. |
| Detect duplicates during record entry and merge before saving a new duplicate | Supported; the standard duplicate dialog offers merging for Account, Contact, and Lead. Case has a separate native merge experience. | Provides save-time detection and a merge workflow for configured, supported tables, including custom tables. |
| Run detection jobs over existing data | Supports background and scheduled duplicate detection jobs. | Provides filtered, Power Automate-backed detection jobs with a searchable review queue and merge actions for supported tables. |
| Choose the survivor and retained values manually | Supported for Account, Contact, and Lead, including options to show conflicting values and choose populated fields. | Provides side-by-side field selection for supported tables, including custom tables, with comparison fields and order controlled by a configured Dataverse view. |
| Case-sensitive duplicate matching | Supports a case-sensitive rule setting. | Uses Dataverse query matching; case-sensitive string matching is not supported. |


### 1. Express matching logic beyond the standard rule builder

Out-of-the-box rules support exact, first-character, and last-character matching, but combine their conditions using AND and limit each table to five published rules. Supa Merge adds nested AND/OR logic within a FetchXML filter and removes that five-rule restriction from its own engine.

For example, a single rule can find records with the same email address **or** records with both the same name and phone number. Administrators and consultants can combine field placeholders, prefix or suffix matching, and fixed filter criteria to express the organisation's rules without splitting every alternative into a separate rule.

Rules can look for matches within the same table or across different tables—for example, checking whether a new Lead matches an existing Contact. Blank values are ignored by default, with an option to match blanks explicitly. Each rule can be activated or deactivated independently.

Cross-table detection helps users spot related information; merging is available only between records in the same table.

### 2. Extend save-time duplicate resolution to custom tables

The standard experience already warns users about duplicates during record entry, but its duplicate-dialog merge action is limited to Account, Contact, and Lead. Supa Merge brings detection and merge actions together for configured, supported tables, including custom business tables. The review screen groups candidates by table and highlights differing values for same-table comparisons.

When creating a new record, users can apply selected values to an existing same-table record instead of saving another duplicate. They can also choose **Ignore and save** when the record should remain separate. This gives teams an opportunity to resolve duplication at the point of entry while retaining control over legitimate exceptions.

### 3. Merge custom business records—not just standard CRM records

Native merge is limited to Account, Contact, Lead, and Case. Supa Merge extends controlled merging to supported custom tables, so duplicate cleanup can include records such as custom membership or supplier records rather than stopping at standard CRM tables.

Compare two records side by side, select the record that will remain, and choose which field values to retain. The save-time merge experience also includes pending form edits in the comparison.

**Control the merge window with a custom view.** Out-of-the-box merge does not let administrators assign a custom Dataverse view to define its displayed fields. Supa Merge does: configure a view for each merge-enabled table, then choose its columns and their order to shape the comparison. For example, a membership table can show membership number, renewal date, and contact details, helping users make decisions without unrelated fields distracting them. Administrators maintain that field list through the view rather than changing the merge-window code.

Supa Merge supports Account, Contact, Lead, and Case using the platform's native merge operation, and extends merging to supported custom tables. On the custom-table path, eligible related records are moved according to relationship reparenting settings, and the merged-away record is deactivated and linked to the survivor. A notification identifies the surviving record when users open the merged-away record.

If the record you want to keep is inactive, Supa Merge can reactivate it as part of the merge process using configured or metadata-derived status values. The standard merge experience requires that reactivation to happen first as a separate step.

### 4. Review existing duplicates through detection jobs

Out-of-the-box duplicate detection already supports background jobs. Supa Merge adds a review workflow that connects its flexible matching rules with merge actions for supported custom tables as well as standard tables.

Run a job against a filtered set of existing records, such as a recently imported batch or a defined customer segment. The included Power Automate flow processes the job and stores the results for review.

Users can search the results, inspect candidate matches, and resolve same-table duplicates from the review screen. Job status shows whether processing is queued, running, completed, or failed. Bulk detection produces a review queue; it does not automatically merge every match.

### 5. Apply consistent field-selection logic with Auto Merge

The standard merge dialog can select populated fields, but it does not offer a configurable script for business-specific field decisions. Supa Merge's Auto Merge lets a consultant define that logic in server-side JavaScript—for example, copying selected contact details only when the duplicate comes from a source the business trusts. The script returns the fields to copy, so the decision can go beyond simply choosing whichever value is populated.

In the duplicate review screen, users select a saved duplicate and choose **Auto Merge** to execute the merge without making each field selection manually. The current record survives; the script decides which fields to copy from the selected duplicate. Auto Merge requires a configured script and is unavailable for a new, unsaved record. It is a user-triggered action, rather than an unattended deduplication service.

## How It Works

1. **Configure:** An administrator defines detection rules and enables merging for the required tables, including the comparison view and optional Auto Merge script.
2. **Find:** Users encounter matches during a save, review a completed detection job, or select two records directly from a main grid.
3. **Decide:** Users review the pair and choose the surviving record and field values, or invoke configured Auto Merge logic for saved records.
4. **Merge:** Supa Merge applies the selected changes and processes the records through the native or custom-table merge path.

## Deployment and Product Fit

- **Platform:** Designed for Dynamics 365 CE and Dataverse model-driven apps. Detection rules and merge settings require administrator or consultant configuration; advanced matching uses FetchXML and Auto Merge uses JavaScript.
- **Permissions:** Detection and record operations run as the calling user, so matches are limited to records that user can access. Merge users need the global Merge privilege, appropriate table and record access, and Create access to Supa Merge Request. Merge availability checks include Write, Share, and Append To privileges on the configured table.
- **Table and field support:** Merges are same-table only. Elastic tables and File fields are not supported. Custom-table status models and relationship settings should be checked during implementation; related-record movement follows eligible one-to-many relationships, rather than moving every relationship indiscriminately.
- **Application setup:** Bulk detection uses the included Power Automate flow. For Lead and Case, hide the out-of-the-box Merge button using Ribbon Workbench in XrmToolBox as part of setup.

# Configuration

This section is for Power Platform admins setting up the solution.

To use this Apps Gallery Supa Merge solution, you will need to purchase a license and activate it for your Dynamics 365 instance. Please refer to instructions here: https://apps-gallery.dev/Docs/activate-license

## Duplicate Detection Rules

It is recommended to **unpublish** all the OOTB Duplicate Detection rules, and untick the enable duplicate detection table setting (optional). If the OOTB duplicate detection rules are published for tables overlap with tables configured in Supa Merge solution, end users will get two popups when saving the record and create confusion.

Navigate to Apps Gallery Supa Merge Admin model-driven app and select Rules under Duplicate Detection.

![Duplicate Detection Rules](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/DuplicateDetectionRules.png?raw=1)

Create rules for the table that you would like to enable duplicate detection.

![Duplicate Detection Rule Setting](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/DuplicateDetectionRuleSetting.png?raw=1)

The syntax of placeholders and functions to be used in FetchXML Filter Fragment are documented in the User Guide tab, which also includes some common, ready-to-adapt examples.

Admin can either delete or deactivate an existing rule for the engine to ignore the rule.

## Duplicate Detection Job

This is similar to the OOTB duplicate detection job. You create a job and the system will fetch the records using FetchXML Filter fragment to obtain all the records need to be checked for duplicates. The FetchXML Filter fragment can be empty. In this case, the system will fetch all records in Dataverse for a table to run duplicate detection.

![Duplicate Detection Job](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/DuplicateDetectionJob.png?raw=1)

**Note:** The FetchXML Filter fragment here doesn't use dynamic values. You can use FetchXML builder in XRMToolbox to come up with the correct filter element, copy and paste it here.

For example:

``` XML
<filter type="and">
    <condition attribute="ag_name" operator="begins-with" value="Contoso" />
</filter>
```

Once you save the new job record, the status reason will be set to Queue and trigger a Power Automate flow to execute the job.

**Important:** The records that Power Automate flow have access to depends on the Dataverse connection user account's security role. If you have a complex security setup for tables in Dataverse and need the job to go over all records in the table, then the flow's Dataverse connection user account will need a security role that have READ access to all records in the table, or use the OOTB System Administrator security role.

Once the Power Automate starts executing, it will set the Status Reason of this job record to Running.

When the job completed without any errors in Power Automate, the Status Reason will be set to Complete.

If there are errors in Power Automate, then Status Reason will be set to Failed. Admin user will need to check the Power Automate run history to check for errors.

The Results tab shows all the records that were checked in the left pane, and displays the potential duplicates in the right pane.

![Job Results](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/JobResults.png?raw=1)

User can click the arrow icon to open the record being checked in a new browser tab. The Name column in the duplicates pane are also clickable and opens the record in a new browser tab as well.

User can select one of the duplicates and click the Merge button at the bottom to manually merge the two records. Or use the Auto Merge button to automatically merge the record. Auto merge assumes the record being checked is the Master record and the selected duplicate is the subordinate.

## Supa Merge Configuration

In the same Apps Gallery Supa Merge Admin model-driven app, you can find configurations for Supa Merge.

![Supa Merge Config](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/SupaMergeConfig.png?raw=1)

In the configuration record, you can configure below options.

**General Settings**

![Supa Merge Config General](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/SupaMergeConfigGeneral.png?raw=1)

**Auto Merge Setting**

![Supa Merge Config Auto Merge](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/SupaMergeConfigAutoMerge.png?raw=1)

### Merge View Id

This is the unique View GUID of a Dataverse view that contains the columns to be display in the merge screen.

![Merge Screen](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/MergeScreen.png?raw=1)

An admin will create a custom view for the table, and add all the columns you would like to be displayed in the merge screen for selection. Publish the view and optionally ensure this view is **NOT** included in the model-driven app, so that users won't see this view.

### Security Permission Settings

- Grant Full Access to Master Owner
- Grant Shared Access to Subordinate Owner

These two settings minic the OOTB Organization DB settings that affect the OOTB Merge functionality.

These two settings are configurable for tables that OOTB Merge doesn't support, i.e. tables other than Account, Contact, Lead and Case.

For Account, Contact, Lead and Case, please change the Organization DB settings.

https://support.microsoft.com/en-us/servicing/dynamics/crm/hotfix/2020/10/orgdborgsettings-tool-for-microsoft-dynamics-crm

![Org Db Settings](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/OrgDbSettings.png?raw=1)

### Inactive Master Configuration

Supa Merge allows selection of an inactive record as the master record. In this case, the inactive record will be reactivated when merge is executed.

- Reactive Default Status: the statecode option set value (integer) to be set to during activation.

- Reactivate Default Status Reason the statuscode option set value (integer) to be set to during activation.

If these two settings are not set, then the engine makes best guess based on the table metadata. i.e. statecode: Active (0) and statuscode: Active (1) for example.

### Auto Merge Custom Script

This custom script setting accepts a piece of JavaScript that must return an Array of String. Each string is a column's logical name.

The returned array of string determines the **Subordinate's** column values to be used to overwrite the master's columns.

If the script returns NULL or empty string array, it will take all merge view column values from subordinate and overwrite master record.

**Important**: the JavaScript code is executed server-side, not in the browser. The normal Client API syntax for model-drive apps does NOT apply here. However, you do follow JavaScript coding syntax.

The following objects (object name is case-sensitive) are available to use in custom script code:

- masterEntity: This is the entity record that SharePoint folder and document library are generated against. It is equivalent to Entity object in C# and with all columns.
- subordinateEntity: The entity metadata of the target entity record. It is equivalent to EntityMetadata object in C#.
- clientService: This is an instance of IOrganizationService object that you can use to query table data.
- log: This is a shorthand of TracingService.Trace method.

You can also use all Types under System and System.Core namespaces.

**masterEntity** & **subordinateEntity**

If you are creating a new record or modifying an existing record, this record is the masterEntity and the selected record in the Duplicate Detection window is the subordinateEntity.

If you run a Duplicate Detection Job, and select a record in the Left vertical pane, this record is the masterEntity. The record you selected in the Right duplicates pane is the subordinateEntity.

### Get Master or Subordinate Attribute Values

``` JavaScript
var name = masterEntity.Attributes['name']; // string
var primaryContact = masterEntity.Attributes['primarycontactid']; // EntityReference
var industry = masterEntity.Attributes['industrycode']; // OptionSetValue
var industryFormatted = masterEntity.FormattedValues['industrycode']; // string
var creditlimit = masterEntity.Attributes['creditlimit']; // Money
var creditonhold = masterEntity.Attributes['creditonhold']; // bool

log('Master account name: ' + name);
log('Master account entity logical name: ' + target.LogicalName);
log('Master account Id: ' + target.Id.ToString());
log('Master account primary contact Id: ' + primaryContact.Id.ToString());
log('Master account primary contact Name: ' + primaryContact.Name);
log('Master account primary contact Entity Name: ' + primaryContact.LogicalName);
log('Master account industry: ' + industry.Value);
log('Master account industry (formatted): ' + industryFormatted);
log('Master account credit limit: ' + creditlimit.Value);
log('Master account credit on hold: ' + creditonhold);
```

### Retrieve an Entity Record

``` JavaScript
var account2 = clientService.Retrieve('account', new System.Guid('f0969482-6a51-f111-bec6-6045bdc39b78'), new ColumnSet(true));
log('Account 2 name: ' + account2.Attributes['name']);
```

### Execute a Query

``` JavaScript
var query = new QueryExpression('contact');
query.ColumnSet.AddColumns('fullname');
query.Criteria.AddCondition(
    'parentcustomerid',
    ConditionOperator.Equal,
    target.Id
);

var contacts = clientService.RetrieveMultiple(query);
var contact = contacts.Entities[0];

log('First contact name: ' + contact.Attributes['fullname']);
```

### Example Auto Merge Script

``` JavaScript
// Preserve existing master values; fill only missing email and phone.
var fields = [];
var candidates = ["emailaddress1", "telephone1"];
function populated(entity, name) {
    if (!entity.Contains(name)) { return false; }
    var value = entity[name];
    return value !== null && value !== undefined && String(value).trim() !== '';
}
for (var i = 0; i < candidates.length; i++) {
    var name = candidates[i];
    if (!populated(masterEntity, name) && populated(subordinateEntity, name)) {
        fields.push(name);
    }
}
return fields;
```

## Supa Merge Requests

All merge activities performed are stored in this table.

![Supa Merge Request](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SupaMerge/SupaMergeRequest.png?raw=1)

Users who can perform merge will need the global Merge permission as well as Create permission to this Supa Merge Request table.

The security role Apps Gallery Supa Merge User will provide the neccessary permission to users who need to perform Merge.

All rows in this table cannot be updated. Admin can configure a Bulk Deletion Job to delete historical merge request records.