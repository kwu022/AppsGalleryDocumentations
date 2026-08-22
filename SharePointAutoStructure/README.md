# Product URL

https://apps-gallery.dev/Apps/sharepoint-auto-structure

# Purpose

The Out of the Box SharePoint Online integration creates a document library for a Dynamics 365 Customer Engagement table. All the records in the table have their respective folders in that SharePoint document library.

Overtime, when you have many records in the table and uploaded many files for the records, users will see an error message "The number of items in this list exceeds the list view threshold." when navigate to the Documents table of a record.

This is a SharePoint Online service limit, as described here: https://learn.microsoft.com/en-us/troubleshoot/sharepoint/lists-and-libraries/items-exceeds-list-view-threshold.

Another scenario is when you have customizations in SharePoint to break inheritance of a folder in a document library in order to match the security permissions of the respective record in Dynamics 365. You will likely see the following messages:

- You can't share this folder because there are too many items in the folder.
- You can't share this item because too many items have already been shared in this library.

This is another SharePoint Online service limit, as described here: https://learn.microsoft.com/en-us/troubleshoot/sharepoint/lists-and-libraries/error-share-break-inheritance

The solution to both problems is to reduce the number of items in a SharePoint document library. There isn't an Out of the Box feature in Dynamics 365 will allow you to dynamically decide the location of SharePoint document library and folder should be created for the Dynamics 365 record.

Apps Gallery SharePoint Auto Structure addon is here to overcome these problems. It allows a Dynamics 365 admin to define configurable rules that generate the appropriate document library and folder locations in Dynamics 365. The defined rules are evaluated on the fly when user navigates to the Documents tab of a Dynamics 365 record.

# Key Features

- Create document library Per Period (year, quarter, month, week, day or custom)
- Create document library Per Dynamics 365 record
- Create document library using specified number of characters from the primary name attribute of the record
- Create document library using specified number of characters from record's system GUID
- Create document library using custom JavaScript code that will be evaluated at run-time.
- Create folder using a specified naming pattern.
- Create folder using custom JavaScript code that will be evaluated at run-time.

# Configuration

You will need to ensure Document Management setting is configured in Dynamics 365 CE.

## Step 1 - Configure server-based SharePoint integration

In the D365 instance that you want to install SharePoint Auto Structure addon, navigate to the Power Platform Environment Settings model-driven app. Then select Document Management in the left navigation pane.

Click the "Configure server-based SharePoint integration" link as shown in below screenshot.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/Configserverbasedintegration.png?raw=true)

Run through the setup wizard and enter the SharePoint site collection URL that you want to use to store documents.

One Drive setup in wizard is optional, you can safely skip that.

Once the wizard is completed successfully, you can click the SharePoint sites link in above screenshot to verify a SharePoint site record is created.

## Step 2 - Configure document management settings

Navigate to the Power Platform Environment Settings model-driven app again, and go to Document management.

Click the "Document management settings". In the popout window, select the tables that you want to enable SharePoint document management.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/EnableTablesForSP.png?raw=true)

Click Next, you will then enter the SharePoint site collection URL, which is the one you used in Step 1.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/SPUrlValidation.png?raw=true)

Click the Validate URL button to validate the SharePoint URL. Once it is validated, the Next button at th bottom will be enabled.

In the Folder Structure step, leave default value. App Gallery SharePoint Auto Structure addon will intercept this out of the box logic anyway.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/FolderStructure.png?raw=true)

Click Next to finish the setup.

## Step 3 - Create App Registration

Follow instructions in [Create App Registration for SharePoint Integration](https://apps-gallery.dev/Docs/create-app-registration-for-sharepoint-integration) to create an App Registration with certificate for authentication.

This App Registration and the .PFX file will be used in later configuration in Dynamics 365.

## Step 4 - Configure Apps Gallery SharePoint Auto Structure

Ensure you have entered your license key to activate this addon for your Dynamics 365 organization.

Please refer to [Activate License](https://apps-gallery.dev/Docs/activate-license) for instructions.

Navigate to Apps Gallery SharePoint Auto Structure model-driven app.

Select SharePoint Auto Structure Setting under Structure Configuration area in the left navigation pane.

Click + New to create a new setting record.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/NewSAS.png?raw=true)

Select the SharePoint Site from the dropdown, and Save the record.

Once it is saved, you will be presented with extra fields.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/SASConnection.png?raw=true)

Enter the following:

- Tenant Id
- Client Id
- Upload the .pfx file
- Password for the .pfx file. Password will be encrypted after saving the record.

You can find the Tenant Id and Client Id in the App Registration you created in Azure Portal.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/AppRegistration.png?raw=true)

When you save the record, it will test the connection to the selected SharePoint site.

If the connection test was successful, you will see the Status of this setting record become Active. Otherwise, you will be presented with an error.

# Folder Naming Settings

Naming Rules:

- Pattern
- Custom Script

## Pattern

When Pattern rule is selected, you can specify a basic pattern in the Pattern field.

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/FolderPattern.png?raw=true)

- Placeholder {0} is the table schema name
- Placeholder {1} is the system GUID of the record

## Custom Script

When Custom Script is selected, you can enter JavaScript code in the Folder Name Script tab.

The script must return a string value to be used as the folder name.

Please refer to [JavaScript Custom Script](#javascript-custom-script) for examples.

# Library Naming Settings

Naming Rules:

- None
- Period
- Per Record
- Starting Name Characters
- Starting ID Characters
- Custom Script

## None

If None is selected, document library will be generated using table's schema name.

## Period

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/Period.png?raw=true)

You can specify a pattern to be used.

- Placeholder {0} is the table schema name
- Placeholder {1} will be replaced with the calculated value of the selected Period

Period is a dropdown that contains the following options:

- Day: Format the selected Period Data Source value to "yyyy-dd".
- Day and Month: Format the selected Period Data Source value to "yyyy-MMM-dd".
- Week: Format the selected Period Data Source value to "{Year}-W{Week of Year}". Monday is the start of a week.
- Month: Format the selected Period Data Source value to "yyyy-MMM".
- Quarter: Format the selected Period Data Source value to "{Year}-Q{Quarter of Year}".
- Year: Format the selected Period Data Source value to "{Year}".
- Custom: When Custom is selected, you can specify the custom Date and Time format string in placeholder {1} after a colon, like {1:yyyy-MM}. Please refer to [Custom date and time format strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings) for more information.

Period Data Source is the value that will be used to generate the period value.

- UTC Now
- Created On of Current Record


## Per Record

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/PerRecord.png?raw=true)

There are two patterns you can specify

- Pattern field contains two placeholders
    - {0} is the table schema name
    - {1} will be replaced by the calculated value of Record Name Pattern.
- Record Name Pattern also contains two placeholders
    - {0} is the record's primary name attribute value
    - {1} is the record's system GUID

You can also specify a characters in Unknown Character field to replace any special characters in the record's primary name attribute value. If you don't specify anything, special characters will be replaced by empty string.

## Starting Name Characters

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/StartingName.png?raw=true)

You can specify a pattern to be used.

- Placeholder {0} is the table schema name
- Placeholder {1} will be replaced with the Number of Name Characters taken from the record's primary name attribute

Enter an integer for Number of Name Characters, maximun is 100.

You can also specify a characters in Unknown Character field to replace any special characters in the record's primary name attribute value. If you don't specify anything, special characters will be replaced by empty string.

## Starting ID Characters

![alt text](https://github.com/kwu022/AppsGalleryDocumentations/blob/main/SharePointAutoStructure/StartingId.png?raw=true)

You can specify a pattern to be used.

- Placeholder {0} is the table schema name
- Placeholder {1} will be replaced with the Number of Id Characters taken from the record's system GUID without hyphen (-)

Enter an integer for Number of Id Characters, maximun is 32.

## Custom Script

When Custom Script is selected, you can enter JavaScript code in the Library Name Script tab.

The script must return a string value to be used as the document library name.

Please refer to [JavaScript Custom Script](#javascript-custom-script) for examples.

# Other Scripts

In the Other Scripts tab, you can enter JavaScript code to

- **Parent Location Script**: Specify a parent entity record's SharePoint folder in where the current record's folder should be created.
- **Sub-folders Script**: Specify an array of string that represent sub-folders to be created in the current record's folder.

## Parent Location Script

The JavaScript must return

- NULL: folder will be created using the Document Library and Folder settings.
- Entity Reference: current record's folder will be placed in the folder of this entity reference record. A SharePoint folder and document location will be created for the entity reference record if doesn't exist.

Please refer to [JavaScript Custom Script](#javascript-custom-script) for examples.

## Sub-folders Script

The JavaScript must return

- NULL: no sub-folder will be created
- String Array: A string represents the name or path of sub-folder(s). For example, you can return ["subfolder 1", "subfolder 2", "subfolder 3"], or ["Subfolder 1", "Subfolder 2/level 1", "Subfolder 3/level 1/level 2"].

Please refer to [JavaScript Custom Script](#javascript-custom-script) for examples.

# JavaScript Custom Script

Custom script allows you to write custom logics in JavaScript to determine folder name and document library name.

**Important**: the JavaScript code is executed server-side, not in the browser. The normal Client API syntax for model-drive apps does NOT apply here. However, you do follow JavaScript coding syntax.

The following objects (object name is case-sensitive) are available to use in custom script code:

- target: This is the entity record that SharePoint folder and document library are generated against. It is equivalent to Entity object in C# and with all columns.
- targetMetadata: The entity metadata of the target entity record. It is equivalent to EntityMetadata object in C#.
- clientService: This is an instance of IOrganizationService object that you can use to query table data.
- log: This is a shorthand of TracingService.Trace method.

You can also use all Types under System and System.Core namespaces.

## Get target Attribute Values

``` JavaScript
var name = target.Attributes['name']; // string
var primaryContact = target.Attributes['primarycontactid']; // EntityReference
var industry = target.Attributes['industrycode']; // OptionSetValue
var industryFormatted = target.FormattedValues['industrycode']; // string
var creditlimit = target.Attributes['creditlimit']; // Money
var creditonhold = target.Attributes['creditonhold']; // bool

log('Current account name: ' + name);
log('Current account entity logical name: ' + target.LogicalName);
log('Current account Id: ' + target.Id.ToString());
log('Current account primary contact Id: ' + primaryContact.Id.ToString());
log('Current account primary contact Name: ' + primaryContact.Name);
log('Current account primary contact Entity Name: ' + primaryContact.LogicalName);
log('Current account industry: ' + industry.Value);
log('Current account industry (formatted): ' + industryFormatted);
log('Current account credit limit: ' + creditlimit.Value);
log('Current account credit on hold: ' + creditonhold);
```

## Use targetMetadata Values

``` JavaScript
log('Current account primary id attribute: ' + targetMetadata.PrimaryIdAttribute);
log('Current account schema name: ' + targetMetadata.SchemaName);
log('Current account entity set name: ' + targetMetadata.EntitySetName);
log('Current account logical name: ' + targetMetadata.LogicalName);
```

## Retrieve an Entity Record

``` JavaScript
var account2 = clientService.Retrieve('account', new System.Guid('f0969482-6a51-f111-bec6-6045bdc39b78'), new ColumnSet(true));
log('Account 2 name: ' + account2.Attributes['name']);
```

## Execute a Query

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

## Parent Location Script Example

``` JavaScript
if (target.LogicalName === "ag_file")
{
    var parentContactId = target.GetAttributeValue('ag_parentcontactid');
    var parentContactEntity= clientService.Retrieve(parentContactId.LogicalName, parentContactId.Id, new ColumnSet('parentcustomerid'));
    return parentContactEntity.GetAttributeValue('parentcustomerid');
}
else{
    return null;
}
```

## Sub-folders Script Example

``` JavaScript
if (target.LogicalName === "ag_file") {
    const subfolders = ["Apple/Red/Big", "Banana/Yellow/Long", "Orange/Small"];
    return subfolders;
}
else {
    return null;
}
```

In above example, when the current record's logical name is ag_file, it will create 3 subfolders: Apple, Banana and Orange.

Under Apple subfolder, there will be a folder with name Red. And under folder Red, there will be a folder with name Big.

Same applies to Banana and Orange folders.