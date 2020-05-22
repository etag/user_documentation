# User guide to Electronic Transponder Analysis Gateway

## Last updated 21 May 2020
For assistance or bug reports, please contact [Claire Curry](cmcurry@ou.edu), or submit an issue on our [repositories](https://github.com/etag) for the [visualizations and web portal](https://github.com/etag/portal_nuxt), [data import](https://github.com/etag/etagq), or [interacting with the API](https://github.com/etag/etag-api).

# Quick start guide: How do I use the ETAG website? 
The quick-start section is designed for users who need a refresher or want an overview of the process.  This section gives a step-by-step tutorial.  The final section, [In Depth Documentation](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#in-depth-documentation), will describe features in detail.

1. Visit [the ETAG website](https://head.ouetag.org).
1. Get a username and password if you don't have one.  [Contact Claire](mailto:cmcurry@ou.edu) to get a username.  (FIXME: Tyler implementing user management system.)
1. [Log in with your username and password](https://head.ouetag.org/login/) by clicking on the "Log in" button in the upper right corner of the site.
1. Format your files' columns and data using our examples and templates.  The filename itself does not matter (file is not kept - data are transferred to database).
    - Format data following examples:
        - Tagged Data: [example 1](https://osf.io/4m8k2/), [example 2](https://osf.io/hkmce/), [template](https://osf.io/jzf3b/)
        - Reader Data: [example](https://osf.io/wgbty/), [template](https://osf.io/fv5cw/)
        - RFID Reads: [example 1](https://osf.io/t4by2/), [example 2](https://osf.io/t53jf/), [template](https://osf.io/mxtue/)
    - Your files need to have (at minimum) exactly the same column headers and be in .csv format as each example file.
    - Extra columns are acceptable in Tagged Data and RFID Reads and will be kept as "field data" or "accessory data".
    - [See formatting](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#required-fields), for details on what the fields/columns represent and how they must be formatted.  It is easiest to paste your data into the template in a spreadsheet program such as Microsoft Excel or LibreOffice Calculate. 
1. [Upload each file](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#upload-files).
    - Upload first (any order)
        - Tagged Data
        - Reader Data
    - Upload last
        - RFID Reads (you may have multiples of this file type because each reader will generate this file if you have multiple readers)

<kbd><img src="/about_and_logged_in_tabs-data_upload_highlighted.png" alt = "data entry tabs with a rectangle around them" style="width:50%;height:50%; /></kbd>

1. View each data type ([Reader Data](https://head.ouetag.org/readerdata), [RFID Reads](https://head.ouetag.org/rfidreads), [Tagged Data](https://head.ouetag.org/taggeddata)) in tabular format and edit your data as needed.
1. [View your data on the map](https://head.ouetag.org/map) if readers have GPS points.  [Multiple visualizations](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#visualize-data) are available.
1. Export your data via [.csv downloads](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#downloading-your-data).
1. Use your data via [API calls]().
1. Have a question about the details of ETAG functionality?  Read the [In depth documentation](https://github.com/etag/user_documentation/blob/master/User_Guide_for_ETAG.md#in-depth-documentation) or contact our [help wiki](https://osf.io/zbd63/wiki/) (Claire and Eli are notified when changes or comments are made).


# What is ETAG?
The Electronic Transponder Analysis Gateway (ETAG) is a database and software system to provide professional data management and versatile data dissemination to the growing community of researchers who use Radio Frequency Identification (RFID) technology to advance biological inquiries in fields like animal behavior, ecological physiology, and community ecology. ETAG is an infrastructure based on open-source tools, allowing scientists to collect, validate, visualize, analyze, and share data in near real-time. ETAG facilitates new capacities both for producing novel science and for sharing data with fellow researchers and the general public. Our system will free up time from the management of data collection, analysis, and curation (currently done by hand), leaving researchers with more time for science. 

# What is RFID?
RFID is a mature and ubiquitous technology, familiar to people in the form of electronic tool-booths or as 'microchip' tags implanted in cats and dogs. RFID entails short-range wireless communication between small transponder tags and readers, and it can facilitate tracking of individual items or animals that are equipped with a tag. A community of researchers has emerged that employs RFID to track individual birds, mammals, fish, reptiles, and even insects in a wide range of field and laboratory research endeavors.

# Who should use ETAG?
You should use ETAG if you have RFID reads with associated data on the tagged organisms and the reader locations.  Our system requires three types of files: animal metadata, reader metadata, and tag reads.

# Why should I use ETAG instead of my own personal data management system?
- Using ETAG's already designed, standardized database will save you time on managing your own database.
- ETAG provides several visualizations that can be accessed via API for your lab website or outreach.
- Data from all of your studies can be pulled from the database at once with API calls in R or Python.
- Data can be public OR private, allowing you to share data when you're ready.

# How can I help?
- Submit your data to ETAG!
- Tell your colleagues!
- [Donate](mailto:ebridge@ou.edu).  Donations will go towards funding ETAG server and maintenance costs, which are currently about US$60-65 per month.
- Write ETAG server maintenance costs into your budget if you are writing a grant proposal involving RFID data collection.  Please contact [Eli Bridge](mailto:ebridge@ou.edu) for information on current costs and needs.
- Write code!  Please contribute issues, fixes, and ideas to our repositories via pull requests and the Github issue tracker.

# In depth documentation
## Create an account
[Contact Claire](mailto:cmcurry@ou.edu) to get a username.  (FIXME: Tyler implementing user management system.)

## Upload files
Three comma-separated text files (.csv) are required by ETAG for upload.  ETAG understands (parses) data from certain fields to populate the database.

- Tagged Data
- Reader Data
- RFID Reads (needs previous two files uploaded first)


You can upload these data files to ETAG manually (all three) or automatically (RFID Reads only).  Once you have Tagged Data and Reader Locations, you can upload the updated RFID Reads file or additional non-overlapping RFID Reads files as you get more reads.  We will use these filenames, but the filenames are not standardized in the system.  Files are deleted from the server after being put into the database, so your data exists, but only in the database.

### Required fields
Required field names are shown when you download the templates.  Your fields (columns) must have names exactly matching the template's required fields, including capitalization and punctuation such as underscores.  All extra columns in Tagged Data and Reader Data will be put in JSON fields that store data in a single, queryable column per table (for Tagged Data: "Field Data" and Reader Data: "Accessory Data").  These extra columns are where you will put data such as animal measurements or sensor data accompanying tag reads.

### Manually 
Use named tabs to load any of the three files manually.  Tagged Data and Reader Data can only be uploaded manually and must be uploaded before RFID Reads.  If you have uploaded previous Tagged Data or Reader Data, then you can upload new RFID Reads without repeating that step for the same study.

#### Tagged Data
The minimum required fields to be filled are [TAG_ID, ANIMAL_SPECIES, and TAGSTARTDATE](https://github.com/etag/etagq/blob/master/etagq/tasks/tasks.py).  The [template file](https://osf.io/jzf3b/) shows the required headers along with additional standard headers (do not change these names).
##### Upload
When you upload your Tagged Data file, the code checks a list of the user's existing owned tag IDs versus the tag IDs in your .csv file.  The tag_id column is limited to 10 characters.  Please contact [Eli Bridge](mailto:ebridge@ou.edu) and [Claire Curry](mailto:cmcurry@ou.edu) if you use tags with >10 characters (we have not yet encountered such).

If the tag ID doesn't exist, ETAG adds the tag ID to the database.  If the tag exists but you (the user) don't "own" it, you cannot update the data for that tag ID. This would happen if someone else has already uploaded that tag ID (perhaps someone else in your research group, or another research group if you detected their animal). The remainder of your .csv file will upload normally.

##### Correcting and appending records
If the tag ID matches one of your owned tags in the database, ETAG will check all other fields for your Tagged Data file.  If there are differences, ETAG will UPDATE BY OVERWRITING individual tag records.  If you upload a file where you have deleted a record, ETAG will not remove that record from the database - you must delete it manually through the ETAG editing interface.  (ETAG is not comparing the csv files to each other, but matching records from your csv to data that has already been processed into the database.)

If there are multiple rows in your Tagged Data file that have identical tag IDs and tag start dates (i.e., you have multiple records or measurements for one individual), ETAG will update the field data and use the last record for updating non-field data values.  You can [read the code itself to further see logic for updates](https://github.com/etag/etagq/blob/4894da9d4f73a310a5f5a0dcba891dc528629780/etagq/tasks/db_utils.py#L303).

These two behaviors provide a method to correct data via uploads.  You can also use the UI to correct them manually, as for deletions. 

If you want to append data, you MUST upload all previous records plus your appended items. You can export your existing records if you have misplaced your local files using the blue "Download data" button below your records.  Use that as a template to upload the corrected (in this case, appended) records for the tag ID (i.e. for the tagged animal/item).

#### Reader Data
Reader Data does not require a GPS point, but RFID Reads will only be available for visualization if GPS points are provided.  The tag ID is the RFID tag identifying number.  This is limited to 10 characters.  The UUID is the reader identifying number (i.e., the reader's "name").  If you don’t have a reader UUID, we recommend using your username (which is required to be unique) and adding sequential numbers after it for each reader.  Start and end date columns allow for you to use the same reader for different projects by specifying when the reader should be associated with which RFID read data.


#### Tag reads
Tag reads from 2019 or later Bridge Lab ETAG readers should conform to the ETAG database formatting standards and need no modification.  Output files from older Bridge lab or third-party readers likely will not conform to the ETAG database upload standards.  Please compare your files to the template files or to your exported files, make appropriate formatting changes to a copy of your original data, and upload the revised copies.

Time stamps must be in the formats described in the database documentation section [8.5.1.3. Time Stamps](https://www.postgresql.org/docs/9.3/datatype-datetime.html#DATATYPE-TIMESTAMPS)

If you make changes to your tag reads file in Excel, beware Excel's automatic csv import.  Manually set Excel to import everything as text.  Otherwise, Excel will change the date formatting or drop leading zeroes from RFID tag numbers.  An alternative is using R to add a column with the reader UUID (reader name).

### Automatically
You can upload RFID Reads automatically to the ETAG portal using the API and your authentication token.  Duplicates should not occur because loading occurs real-time.  Tagged Data and Reader Data files must be uploaded manually before you allow RFID Reads to attempt loading.  This feature is in development and not currently available.

#### Wired connection
In development.

#### Wireless connection
[In development](https://osf.io/5dh3q/)

## Exports, downloads, and backups
You will likely want to download your data to use in local analyses or as a backup.  Here we describe how you can download your data and how we backup your data in the cloud and physically at the University of Oklahoma.

### Downloading your data
You can export and download your data as three .csv files (RFID Reads, Tagged Data, and Reader Data) from each tab (Reader Data, RFID Reads, and Tagged Data, respectively) by clicking on the "Download Data" button (bottom right).

### ETAG automated backups
The primary ETAG repository resides within Amazon Web Services (AWS) Relational Database Services (RDS).  The ETAG system will maintain an off-site backup copy of all data through daily backups with AWS Simple Storage Service (S3), which roll-over every seven (7) days (i.e., only the last seven days are kept).

ETAG will generate two tape copies of all data on a monthly basis within the University of Oklahoma (OU) OURRstore (FIXME: needs implementation).

With three storage locations (main on AWS RDS, daily rolling backups on AWS S3, and monthly static on AWS S3), even a simultaneous and catastrophic failure in 2/3 of facilities will not result in the loss of ETAG data.  Hopefully, most users will also keep local copies of their data for 4 locations for any given dataset.

## Accessing data with the API
### Authorization to access the API 
To access public information (as in R example below), no API token is needed.  To access private information (the default data upload setting), the API call will need to include the user's api token for 
authentication. This token can be accessed at: https://head.ouetag.org/api/user under the "auth-token" field. This token needs to be 
included in the header of the API request. 

### API access code.
Run code from your preferred platform.  We provide sample code for [R API calls](https://osf.io/qe53h/) and [Python API calls](https://osf.io/pz7ej/).  You can also use Bash as in the below example.
    curl -X POST --data-ascii 
    '{"function":"etagq.tasks.tasks.etagDataUpload","queue":"celery","args":[],"kwargs":{ },"tags": []}' https://head.ouetag.org/api/queue/run/etagq.tasks.tasks.etagDataUpload/?format=json -H Content-Type:application/json -H 'Authorization: Token yourauthcodehere'

### Syntax and specifics
The API supports the following methods for getting and setting values: POST, PUT, GET.  To receive JSON serialized data, include "format=json" as part of the query. For example: 
https://ec2-54-186-103-38.us-west-2.compute.amazonaws.com/api/user/?format=json
.csv format is not supported directly via the API at this time.

### Examples
Here is an example of querying the locations for reader "T2B" on the test instance: https://ec2-54-186-103-38.us-west-2.compute.amazonaws.com/api/etag/reader_location/?reader_id=T2B

Endpoints can be queried by supplying a field and value to filter on; with 
multiple filters separated with an "&". For example: https://ec2-54-186-103-38.us-west-2.compute.amazonaws.com/api/etag/tag_reads/?reader_id=TU109876&tag_id=TU0000720

## Visualize data
The ETAG portal currently offers two data types, two options for tag read displays, and four filters.
- Data types
    - Readers
    - Tag reads
- Tag reads display options
    - Summaries (count per location)
    - Raw tag reads Individual reads
- Filter by
    - Species
    - RFID tag ID
    - Data privacy (all public data or only your data)
    - Date minimum and maximum

You can feature visualizations on your own website by pulling from the ETAG API.  Even if you are logged into the main ETAG site, if you want to view the [ETAG API directly in your browser](https://head.ouetag.org/api/) you will need to log in again to view your data.  For example, [sample R code to call from the API](https://osf.io/qe53h/) could be used in combination with an [RShiny site](https://shiny.rstudio.com/).  We encourage sharing and welcome contributions via pull requests or issues to our [in development visualization code](https://osf.io/8gwjz/).  

## Design a RFID antenna (FIXME: in progress)
The "Antenna" tab allows you to input parameters and see the resulting RFID antenna.  Please contact Dr. J. Ruyle (ruyle@ou.edu) or Dr. E. Bridge (ebridge@ou.edu) if you have questions about antenna design.  Please add an issue to portal_nuxt regarding [this page](https://github.com/etag/portal_nuxt/blob/test/pages/antenna.vue) if you have suggested modifications to the antenna visualization.
