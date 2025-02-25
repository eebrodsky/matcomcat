Introduction
------------

matcomcat is a Matlab package, intended (initially) as a demonstration of Matlab code
used to search the ANSS ComCat Earthquake Catalog.  It currently consists of one class, LibComCat, which
<<<<<<< HEAD
is a wrapper around the ANSS ComCat search  <a href="http://earthquake.usgs.gov/fdsnws/event/1/">API</a>, and
two functions:

- LoadComCat which batch queries ComCat searches to circumvent the 20,000 event limit.
=======
is a wrapper around the ANSS ComCat search  <a href="http://comcat.cr.usgs.gov/fdsnws/event/1/">API</a>, and
two functions:

- LoadComCat which does a search with fewer input parameters.
>>>>>>> 84582de3c520a8dc5e4f17c352e934a5278c7a3e
- readcomcat which parses the CSV output by the ComCat web site into a structure array. 

Installation and Dependencies
-----------------------------

This package depends on:
 * p_json, which can be found here: 
http://www.mathworks.com/matlabcentral/fileexchange/25713-highly-portable-json-input-parser/content/p_json.m

* To install this package, you can either use git to clone the following url:
https://github.com/mhearne-usgs/matcomcat.git

or download the zip file of the repository from:
https://github.com/mhearne-usgs/matcomcat/archive/master.zip

or by clicking the "Download ZIP" button found on:
https://github.com/mhearne-usgs/matcomcat

Any directory created using the above methods should be added to the Matlab path.

Uninstalling and Updating
-------------------------

To uninstall:

Delete the directory created by any of the above installation methods.

To update:

If the initial directory was created by using "git clone", then you can update
by doing:

git pull

in the directory.

For either of the other two methods, uninstall as above and reinstall using your preferred approach.

Usage
------------
<pre>This class is a wrapper around the ComCat search API:
 http://earthquake.usgs.gov/fdsnws/event/1/
 It provides methods for retrieving data from ComCat.
 
  getCatalogs - Retrieve a cell array of available product catalogs.
  lbc = LibComCat();
  catalogs = lbc.getCatalogs();
  Output:
   - catalogs is a cell array of available product catalogs
 
  getEventData - Retrieve a cell array of event data from Comcat.
  lbc = LibComCat();
  events = lbc.getEventData(varargin);
  Input:
  - varargin is a list of parameters and values:
             - starttime Matlab datenum object
             - endtime   Matlab datenum object
             - xmin Minimum longitude (dec degrees)
             - xmax Maximum longitude (dec degrees)
             - ymin Minimum latitude (dec degrees)
             - ymax Maximum latitude (dec degrees)
             - minmag Minimum magnitude
             - maxmag Maximum magnitude
  Output:
   - events is a cell array of event structures, where
              the interesting fields are:
              - id: Event id
              - properties: Structure with a set of event
              properties
              - geometry: Structure containing a field called
                 'coordinates', a 3 element cell array of lat,lon,depth
  Usage:
  Retrieve all events greater than 5.5 in the last 30 days
  lbc = LibComCat();
  comevents = lbc.getEventData('starttime',now-30,'endtime',now,'minmag',5.5);
  for i=1:length(comevents)
      [yr,mo,dy,hr,mi,se] = unixsecs2date(comevents{i}.properties.time/1000); %unix time stamp in ms
      etimestr = datestr([yr mo dy hr mi se]);
      fprintf('%s - %s\n',etimestr,comevents{i}.properties.title);
  end
</pre>

<pre>
<<<<<<< HEAD
LOADCOMCAT         Batch query ComCat searches to get around NEIC 20,000 event limit
        [YEAR, MONTH, DAY, HOUR, MINUTE, SEC, LAT, LONG, DEPTH,
        MAG, MAGTYPE] = LOADCOMCAT(STARTTIME,ENDTIME,MINMAGNITUDE)
        returns results of a global catalog search within the time
        frame STARTTIME and ENDTIME, for events with magnitude
        greater than MINMAGNITUDE.

        [YEAR, MONTH, DAY, HOUR, MINUTE, SEC, LAT, LONG, DEPTH,
        MAG, MAGTYPE] = LOADCOMCAT(STARTTIME,ENDTIME,MINMAGNITUDE,
        [MINLAT MAXLAT MINLON MAXLON]) performs a search within the
        specified lat/long box.

        STARTTIME and ENDTIME must be entered in serial date
        number format, e.g. STARTTIME = datenum('2014-01-01 00:00:00')

        For searches that will return more than 20,000 events,
        this code will perform multiple ComCat searches, in
        series, and return the aggregated results.  Results will
        be sorted in time, from oldest to newest events.

        Uses the ComCat search API.  For more info see: 
        https://earthquake.usgs.gov/fdsnws/event/1/

        Authors: Morgan Page and Justin Rubinstein
                 U. S. Geological Survey
        Last modified: May 2015
=======
LoadComCat         Batch query ComCat searches to get around NEIC 20,000 event limit
         [YEAR, MONTH, DAY, HOUR, MINUTE, SEC, LAT, LONG, DEPTH,
         MAG, MAGTYPE] = LoadComCat(STARTTIME,ENDTIME,MINMAGNITUDE)
         returns results of catalog search within the time frame
         STARTTIME and ENDTIME, for events with magnitude 
         greater than MINMAGNITUDE.
 
         STARTTIME and ENDTIME must be entered in serial date
         number format, e.g. STARTTIME = datenum('2014-01-01 00:00:00')
  
         For searches that will return more than 20,000 events,
         this code will perform multiple ComCat searches, in
         series, and return the aggregated results.  Results will
         be sorted in time, from oldest to newest events.
 
         Uses the ComCat search API.  For more info see: 
         http://comcat.cr.usgs.gov/fdsnws/event/1/
 
         Author: Morgan Page, U. S. Geological Survey
         Last modified: March 2014
>>>>>>> 84582de3c520a8dc5e4f17c352e934a5278c7a3e
</pre>

<pre>
readcomcat - Read CSV files as generated by ComCat search API.
    data = readsmgrid(csvfile);
    Input:
     - csvfile is a valid filename for a ComCat CSV file.
    Output:
     - data is a Matlab structure array, with each element containing fields:
       - time Matlab datenum of origin time.
       - lat  Latitude of origin.
       - lon  Longitude of origin.
       - depth Depth of origin.
       - mag   Magnitude of origin.
       - magtype Magnitude type (Mb, Ms, etc.)
       - nst     Number of stations used to determine the solution.
       - dmin    ??
       - rms     Root mean square error of ??
       - net     Contributing network of origin.
       - id      Event id
       - updated Matlab datenum Time of most recent origin update.
       - place   String indicating location of epicenter.
       - type    Usually earthquake, but may be mine collapse, mining explosion, etc.
<<<<<<< HEAD
</pre>
=======
</pre>
>>>>>>> 84582de3c520a8dc5e4f17c352e934a5278c7a3e
