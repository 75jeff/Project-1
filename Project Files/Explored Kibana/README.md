Clicking the sample web log data to Kibana web site.


![images](images/Sample data.png?raw=true)



Questions and its answers:

1. In the last 7 days, how many unique visitors were located in India?
    - 237 unique visitors

2. In the last 24 hours, of the visitors from China, how many were using Mac OSX?
    - 5 unique visitors

3. In the last 2 days, what percentage of visitors received 404 errors? How about 503 errors?
    - 94.444% of visitors recieved 404 errors
    - 5.555% of visitors got 503 errors

4. In the last 7 days, what country produced the majority of the traffic on the website?
    - China

5. Of the traffic that's coming from that country, what time of day had the highest amount of activity?
    - 12:00:00.0

6. List all the types of downloaded files that have been identified for the last 7 days, along with a short description of each file type (use Google if you aren't sure about a particular file type).
    - documents: a readable data (ex. *.txt files..)
    - gz: gzip file compression
    - css: style sheet language (html)
    - zip: file compression
    - deb: software package format for Debian Linux distributions
    - rpm: Linux installation package

AT chart Unique Visitors Vs. Average Bytes:

7. Locate the time frame in the last 7 days with the most amount of bytes (activity).
    - 15:00:00.0
  
8. In your own words, is there anything that seems potentially strange about this activity?
    - downloading files

9. Filter the data by this event.

    a. What is the timestamp for this event? 
      - April 1, 2022 @ 18:00:00.0 to April 1, 2022 @ 21:00:00.0
      
    b. What kind of file was downloaded? 
      - documents
       
    c. From what country did this activity originate? 
      - China
      
    d. What HTTP response codes were encountered by this visitor? 
      - 404 code

10. Switch to the Kibana Discover page to see more details about this activity.

    a. What is the source IP address of this activity? 
      - 132.186.182.124
      
    b. What are the geo coordinates of this activity? 
      - {"lat":57.04713806, "lon":-135.3615983}
    
    c. What OS was the source machine running? 
      - ios (iphone OS)
       
    d. What is the full URL that was accessed? 
      - HTTP://elastic-elastic-elastic.org/people/type:astronauts/name:william-s-macarthur/propile

11. From what website did the visitor's traffic originate?
    - elastic-elastic-elastic.org

Finish your investigation with a short overview of your insights.

12. What do you think the user was doing?
    - downloading files

13. Was the file they downloaded malicious? If not, what is the file used for?
    - maybe educational purposes

14. Is there anything that seems suspicious about this activity?
    - it is against the confidentiality of information

15. Is any of the traffic you inspected potentially outside of compliance guidlines?
    - referer	http://www.elastic-elastic-elastic.com/success/daniel-brandenstein
