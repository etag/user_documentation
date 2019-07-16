# User guide to Electronic Transponder Analysis Gateway

## Last updated 16 July 2019
For assistance or bug reports, please contact Claire Curry (cmcurry@ou.edu), or submit an issue on one of the repositories at https://github.com/etag .

### Fixme: put this text or link to it from ETAG main page.
### Fixme: screenshots after UI complete.
### Fixme: check if location is required - specified in schema


# Quick start guide: How do I use the ETAG website?

1. Visit https://head.ouetag.org. 
2. Log in with your username and password.
2. Format three files following these templates and examples.
  - Tagged Data [template][3] example
  - Reader Data [template][4] example
  - RFID Reads [template][5] [example][6]
3. Upload each file.
4. View your data (FIXME).

# In depth documentation
# What is ETAG?
The Electronic Transponder Analysis Gateway (ETAG) is a database and software system to provide professional data management and versatile data dissemination to the growing community of researchers who use Radio Frequency Identification (RFID) technology to advance biological inquiries in fields like animal behavior, ecological physiology, and community ecology. ETAG is an infrastructure based on open-source tools, allowing scientists to collect, validate, visualize, analyze, and share data in near real-time. ETAG facilitates new capacities both for producing novel science and for sharing data with fellow researchers and the general public. Our system will free up time from the management of data collection, analysis, and curation (currently done by hand), leaving researchers with more time for science. 

# What is RFID?
RFID is a mature and ubiquitous technology, familiar to people in the form of electronic tool-booths or as 'microchip' tags implanted in cats and dogs. RFID entails short-range wireless communication between small transponder tags and readers, and it can facilitate tracking of individual items or animals that are equipped with a tag. A community of researchers has emerged that employs RFID to track individual birds, mammals, fish, reptiles, and even insects in a wide range of field and laboratory research endeavors.

# Who should use ETAG?
You should use ETAG if you have RFID reads with associated data on the tagged organisms and the reader locations.  Our system requires three types of files: animal metadata, reader metadata, and tag reads.

# Why should I use ETAG instead of my own personal data management system?
- Using ETAG's already designed, standardized database will save you time on managing your own database.
- ETAG provides several visualizations that can be accessed via API for your lab website or outreach.
- Data can be public OR private, allowing you to share data when you're ready.

## Create a (free!) account (FIXME)

## Upload files
Three comma-separated text files (.csv) are required by ETAG for upload.  ETAG understands (parses) data from certain fields to populate the database.

- Tagged Data
- Reader Data
- RFID Reads


You can upload these data files to ETAG manually (all three) or automatically (RFID Reads only).  Once you have Tagged Data and Reader Locations, you can upload the updated RFID Reads file as you get more reads.  We will use these filenames, but the filenames can be as you choose.

### Required fields
Required fields are shown when you download the template from ETAG.  Your fields (columns) must have names exactly matching the template's required fields.  The template file is only shown when you do not have updates.  All extra columns in Tagged Data and Reader Data will be put in JSON fields that store data in a single, queryable column per table (for Tagged Data and Reader Data).  These extra columns are where you will put data such as animal measurements or sensor data accompanying tag reads.

### Manually 
Use the upload tab to load the three files.  Tagged Data and Reader Data are only uploaded manually.

#### Tagged Data
##### Upload
When you upload your Tagged Data file, the code checks a list of the user's existing owned tag IDs versus the tag IDs in the csv.

If the tag ID doesn't exist, ETAG adds the tag ID to the database.  If the tag exists but the user doesn't own it, you cannot update the data for that tag ID.  The API currently gives an error (FIXME: Tyler will add what the message is) but not the user interface (UI), so for you as an end user it will simply not upload.  The remainder of your csv file will upload normally.

##### Correcting and appending records
If the tag ID matches one of your owned tags in the database, ETAG will check all other fields for your Tagged Data file.  If there are differences, ETAG will UPDATE BY OVERWRITING.

If there are multiple rows in your Tagged Data file that have identical tag IDs (i.e., you have multiple records or measurements for one individual), ETAG will update the field data (FIXME: in progress for implementation).

These two behaviors provide a method to correct data via uploads.  You can also use the UI to correct them manually. 

If you want to append data, you MUST upload all previous records plus your appended items. You can export your existing records if you have misplaced your local files using the blue "Download data" button below your records.  Use that as a template to upload the corrected (in this case, appended) records for the tag ID (i.e. for the tagged animal/item).

#### Reader Data
Reader Data does not require a GPS point, but will only be available for visualization if GPS points are provided.

#### Tag reads
Tag reads from 2019 or later Bridge Lab ETAG readers should conform to the ETAG database formatting standards and need no modification.  Output files from older Bridge lab or third-party readers may not conform to the ETAG database upload standards.  Please compare your files to the template files or to your exported files, make appropriate formatting changes to a copy of your original data, and upload the revised copies.

Time stamps must be in the formats described in the database documentation section [8.5.1.3. Time Stamps][7]

If you make changes to your tag reads file in Excel, beware Excel's automatic csv import.  Manually set Excel to import everything as text.  Otherwise, Excel will change the date formatting or drop leading zeroes from RFID tag numbers.  An alternative is using R to add a column with the reader UUID (reader name).

### Automatically
You can upload RFID Reads automatically to the ETAG portal using the API.  Duplicates should not occur because loading occurs real-time.  Tagged Data and Reader Data files must be uploaded manually before you allow RFID Reads to attempt loading.

#### Wired connection
In development.

#### Wireless connection
[In development] [1]

## Exports, downloads, and backups
You will likely want to download your data to use in local analyses or as a backup.  Here we describe how you can download your data and how we backup your data in the cloud and physically at the University of Oklahoma.

### Downloading your data (FIXME: currently needs work on separating columns, so do not test this part)
You can download each data type (RFID Reads, Tagged Data, and Reader Data) as a .csv file from the three pages within the 'My ETAG Data' tab.

### ETAG automated backups
The primary ETAG repository resides within Amazon Web Services (AWS) Relational Database Services (RDS).  The ETAG system will maintain an off-site backup copy of all data through the AWS Simple Storage Service (S3)

ETAG will generate two tape copies of all data on a weekly basis within the University of Oklahoma (OU) Petastore (FIXME: needs implementation)

With three storage locations (main on AWS RDS,  backups on AWS S3, and weekly on the OU Petastore), even a simultaneous and catastrophic failure in 2/3 facilities will not result in the loss of ETAG data.

## Visualize data (FIXME: needs implementation)
The ETAG portal currently offers three filters and two map types.
- Filter by
  - Species
  - RFID reader
  - RFID tag ID
- Map types
  - Summary of counts
  - Individual reads

You can feature visualizations on your own website in Javascript Leaflet by pulling from the ETAG API.  We encourage sharing and welcome contributions to our [in development visualization code][2].  

## Design a RFID antenna (FIXME: in progress)
The "Antenna" tab allows you to input parameters and see the resulting RFID antenna.  Please contact Dr. J. Ruyle (ruyle@ou.edu) or Dr. E. Bridge (ebridge@ou.edu) if you have questions about antenna design.

[1] https://osf.io/5dh3q/
[2] https://osf.io/8gwjz/
[3] https://osf.io/jzf3b/
[4] https://osf.io/fv5cw/
[5] https://osf.io/mxtue/
[6] https://osf.io/znd7u/
[7] https://www.postgresql.org/docs/9.3/datatype-datetime.html#DATATYPE-TIMESTAMPS