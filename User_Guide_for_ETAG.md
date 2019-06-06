# User guide to Electronic Transponder Analysis Gateway

## Last updated 18 April 2019
For assistance or bug reports, please contact Claire Curry (cmcurry@ou.edu), or submit an issue on one of the repositories at https://github.com/etag .

# What is ETAG?
The Electronic Transponder Analysis Gateway (ETAG) is a database and software system to provide professional data management and versatile data dissemination to the growing community of researchers who use Radio Frequency Identification (RFID) technology to advance biological inquiries in fields like animal behavior, ecological physiology, and community ecology. ETAG is an infrastructure based on open-source tools, allowing scientists to collect, validate, visualize, analyze, and share data in near real-time. ETAG facilitates new capacities both for producing novel science and for sharing data with fellow researchers and the general public. Our system will free up time from the management of data collection, analysis, and curation (currently done by hand), leaving researchers with more time for science. 

# What is RFID?
RFID is a mature and ubiquitous technology, familiar to people in the form of electronic tool-booths or as 'microchip' tags implanted in cats and dogs. RFID entails short-range wireless communication between small transponder tags and readers, and it can facilitate tracking of individual items or animals that are equipped with a tag. A community of researchers has emerged that employs RFID to track individual birds, mammals, fish, reptiles, and even insects in a wide range of field and laboratory research endeavors.

# Who should use ETAG?
You should use ETAG if you have RFID reads with associated data on the tagged organisms.

# Why should I use ETAG instead of my own personal data management system?
- Using ETAG's already designed, standardized database will save you time on managing your own database
- ETAG provides several visualizations that can be accessed via API for your lab website or outreach
- Data can be public OR private, allowing you to share data when you're ready.

# How do I use the ETAG website?

General overview and diagram.

## Create a (free!) account

## Upload files
Three files are required by ETAG for upload.  ETAG understands (parses) data from certain fields to populate the database.

- RFID reads
- Animals
- Reader locations

You can upload these data files to ETAG manually (all three) or automatically (RFID reads only).

### Required fields
All extra columns in Animals and Reader Locations will be put in a JSON field that stores data in a single, queryable column.
#### RFID reads
#### Animals
#### Reader locations

### Manually 
Use the upload tab to load the three files.  Visit our OSF page to see example data formatted correctly.  *LINK HERE*.

#### Animals
##### Upload
When you upload your animals.csv file, the code checks a list of the user's existing owned tag ids versus the tag ids in the csv.

If the tag ID doesn't exist, ETAG adds the tag ID to the database.  If the tag exists but the user doesn't own it, you cannot update the data for that tag ID.  The API currently gives an error (FIXME: Tyler will add what the message is) but not the UI, so for you as an end user it will simply not upload.  The remainder of your csv file will upload normally.

##### Correcting and appending records
If the tag ID matches one of your owned tags in the database, ETAG will check all other fields for your animals.csv file.  If there are differences, ETAG will UPDATE BY OVERWRITING.

If there are multiple rows in your animals.csv file that have identical tag IDs (i.e., you have multiple records or measurements for one individual), ETAG will update the field data (FIXME: in progress for implementation).

These two behaviors provide a method to correct data via uploads.  You can also use the UI to correct them manually. 

If you want to append data, you MUST upload all previous records plus your appended items.  You can export your existing records if you have misplaced your local files, and use that template to upload the corrected (in this case, appended) records for the tag ID (i.e. for the tagged animal).

#### Tag reads

### Automatically loading

Duplicates should not occur because loading occurs real-time.

#### RFID read data from Bridge lab ETAG reader after 2019.
The RFID reads from these readers should conform to the ETAG database upload standards and need no modification.

#### Legacy or third-party read data
The RFID reads from these readers may not conform to the ETAG database upload standards.

### Automatically
You can upload RFID reads automatically to the ETAG portal using the API.
#### Wired connection

#### Wireless connection

## Download and back up data
You will likely want to download your data to use in local analyses or as a backup.  You can download your full dataset as a .zip file containing comma separated value (.csv) text files using the download tab/button.

The primary ETAG repository resides within the Amazon Web Services RDS (Relational Database Services).  The ETAG system will maintain an off-site backup copy of all data through the Amazon Simple Storage Service (S3). ETAG will also generate two tape copies of all data on a weekly basis within the OU Petastore. Hence, a catastrophic failure of either or both primary storage facilities will not result in the loss of all ETAG data.

## Visualize data
The ETAG portal currently offers three filters and two map types.
- Filter by
  - Species
  - RFID reader
  - RFID tag ID
- Map types
  - Summary of counts
  - Map of individual reads

You can also pull data to your own website via the API and create your own web visualizations in Javascript Leaflet pulling from the ETAG API.  We encourage sharing and welcome contributions to our visualization code on github.  

## Design a RFID antenna
The "Antenna" tab allows you to input parameters and see the resulting RFID antenna.  Please contact Dr. J. Ruyle (ruyle@ou.edu) or Dr. E. Bridge (ebridge@ou.edu) if you have questions about antenna design.
