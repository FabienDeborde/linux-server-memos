#Wapiti

- Install Wapiti
    - **sudo apt-get install wapiti**
- Scan the website
    - **wapiti http://example.org -n 10 -b folder**
    - *-n 10 limits the number of URLs with the same pattern to 10 (prevent endless loop)*
    - *-b folder sets the scope only to the given domain*
- Download a copy of the generated\_report which should be ~/.wapiti/generated\_folder
- Check the html page to see if there is any vulnerabilities
