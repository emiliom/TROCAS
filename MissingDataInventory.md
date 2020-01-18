## TROCAS Missing-Data Inventory 

Listing of missing sensor files or issues with specific files. Last update: 2020-1-18


### TR 1
- 2019-8-29: **Licor** `transect01_11_2014_7.txt` has 241,474 observations, more than twice the number as the file with the next highest number. If that means it actually goes over > 24 hours, my assumption for handling the midnight roll over breaks down
- 2019-8-29: **Picarro** files are missing

### TR 2
- 2019-8-29: **EXO Sonde** file `Sonde Transects/Upstream/All Upstream.xlsx` is big; I suspect it may aggregate other Sonde files also found in that directory. In that case, it adds a duplication. I've renamed it temporarily, to prevent it being read.
- 2019-8-29: Two **Picarro** files have corrupted TIME values; they're in the form of 48:49.7, with a single colon, the first part not being a proper hour. Will try to read date-time information instead from one of the other time columns, like EPOCH_TIME. The files are: `CFIDS2061-20141107-071220Z-DataLog_User.dat` and `CFIDS2061-20141108-093330Z-DataLog_User.dat`

### TR 3
- 2019-8-29: For **Licor** file `Santarem 7_8_15a.txt`, I corrected the first header row from """2015-07" -08 at "08:39""" to "2015-07-08 at 08:39"; and in second header row, Time(H:M        :S)  CO2    (ppm) to Time(H:M:S)  CO2(ppm). But in the end I've excluded this file b/c the data rows are corrupted (have two extra columns) starting in row 2075.
- 2019-8-29: **EXO Sonde** files are missing (2020-1-18: or largely missing?)

### TR 5
- 2019-8-29: **Licor**:
  - `Tidal/Surface` directory has no .txt files, just .xlsx files. So, I can't ingest it as the other files.
  - `diel/diel_ 11_8_16 Sika.txt` and `Tidal/50 percent depth/50Depth_NMCP_11_8_16.txt` are non-standard. They nare very different from conventional files, having no header rows and 3 columns like this: <incremental int counter>  Time(H:M:S)   CO2(ppm). I can't ingest them.


### TR 8
- 2020-1-18: **EXO Sonde** data was exported in a format that's different from EXO Sonde files from all other TROCAS: in csv rather than Excel format; header rows are organized very differently. We need the .bin files to then use the Sonde software to re-export to the Excel format.
- **Picarro** data was not collected


### General issues, by sensor type
#### EXO Sonde
- Dates may be reversed (YYYY-DD-MM vs YYYY-MM-DD) in some files. In TROCAS 6, see "2017-05-01" vs "2017-01-05"
- A variety of datetime columns occur, apparently added manually and sometimes including duplicate column names. Columns sometimes include one called “datetime” which collided with the datetime name I was using for the final, processed column name. I renamed the new column to date_time.

#### Picarro
- Are times in UTC or Brasilia TZ?
- For now, to handle the large-file (and memory) issue, I'm dropping many of the columns not being used directly.