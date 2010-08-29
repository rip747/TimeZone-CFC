LICENSE 
Copyright 2007 Paul Hastings

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

===   
Included in this archive are three versions of the timezone.CFC to handle various timezone functions:

timezone.cfc: based on core java
icu4jTZ.cfc: based on ICU4J lib's com.ibm.icu.util.TimeZone for installs that have the ICU4J jar file on the server's classpath. requires ICU4J library.
REMOTEicu4jTZ.cfc: based on ICU4J lib's com.ibm.icu.util.TimeZone for installs that do not have the ICU4J jar file on the server's classpath.  requires ICU4J library & mark mandel's javaLoader CFC http://javaloader.riaforge.org/.

note: The two ICU4J based CFCs require an init (mainly to keep the syntax for both CFCs the same). For the remote classpath CFC, you can pass in the location of the ICU4J jar file.

public methods in the CFCs:
- isDST determines if a given date & timezone are in DST. if no date or timezone is passed
the method defaults to current date/time and server timezone. PUBLIC.
- getAvailableTZ returns an array of available timezones on this server (ie according to server's ICU4J version). 
- getTZByOffset returns an array of available timezones on this server (ie according to server's ICU4J version) with the same UTC offset.
- isValidTZ determines if a given timezone is valid according to getAvailableTZ.
- usesDST determines if a given timezone uses DST.
- getRawOffset returns the raw (as opposed to DST) offset in hours for a given timezone. 
- getTZOffset returns offset in hours for a given date/time & timezone, uses DST if timezone uses and is currently in DST.
- getDST returns DST savings for given timezone.
- castToUTC return UTC from given datetime in given timezone. required argument thisDate, optional argument thisTZ valid timezone ID, defaults to server timezone.
- castfromUTC return date in given timezone from UTC datetime. required argument thisDate, optional argument thisTZ valid timezone ID, defaults to server timezone.
- castToServer returns server datetime from given datetime in given timezone. required argument thisDate valid datetime, optional argument thisTZ valid timezone ID, defaults to server  timezone.
- castfromServer return datetime in given timezone from server datetime. required argument thisDate valid datetime, optional argument thisTZ valid timezone ID, defaults to server 	timezone.
- getServerTZ returns server timezone.
- getServerTZShort returns "short" name for the server's timezone.
- getServerId returns ID for the server's timezone (timezone.CFC ONLY)


The ICU4J-based CFCs also include:
- getTZByCountry returns an array of available timezones on this server (ie according to 
server's ICU4J version) within a given country.
- init, initializes the CFC. for non-classpath installs, pass in location to ICU4J jar file. for classpath installs, use a null init.

classpath:
<cfscript>
tz=createObject("component","icu4jTZ").init();
timezones=tz.getTZByCountry("AU");
</cfscript>

non-classpath:
<cfscript>
tz=createObject("component","REMOTEicu4jJTZ").init("c:\resources\icu4j.jar");
timezones=tz.getTZByCountry("AU");
</cfscript>


If you like, you can find my wishlist at 
http://www.amazon.com/gp/registry/wishlist/35SOQPL36CP87/104-4400936-8795966
