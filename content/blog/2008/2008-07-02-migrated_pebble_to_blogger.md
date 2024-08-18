+++
title = 'Migrated pebble to blogger'
date = 2008-07-02
publishdate = 2008-07-02
thumbnail = '/typing.jpg'
+++

Thanks to the guys from google we got a API to post items to our blog. 
Since I've had a pebble blog for some time now, but I don't have access to that server anymore, 
the time had come to use something with less maintenance (read none).


Hereunder you can find the code I've used to migrate the entries. 
Note: There are 2 steps
1. use an xslt to transform the pebble xml to an 'atom' xml.
2. use the python script to upload

The xslt

```xml
<xsl:stylesheet version = '1.0' xmlns:xsl='http://www.w3.org/1999/XSL/Transform'>
    <xsl:template match="/blogs">
        <xsl:for-each select="blogEntry">
            <entry xmlns='http://www.w3.org/2005/Atom'>
                <published><xsl:value-of select="date"/></published>
                <updated><xsl:value-of select="date"/></updated>
                <category scheme="http://schemas.google.com/g/2005#kind" term="http://schemas.google.com/blogger/2008/kind#post"/>
                <title type='text'><xsl:value-of select="title"/></title>
                <content type="html"><xsl:value-of select="body"/></content>
                <author>
                    <name>Koen Serry</name>
                    <uri>http://www.blogger.com/profile/03836830737950982447</uri>
                    <email>koen.serry@gmail.com</email>
                </author>
            </entry>
        </xsl:for-each>
    </xsl:template>
</xsl:stylesheet> 
```

Here is the python script.

```python
import httplib,urllib,re
from string import Template

params = urllib.urlencode({'Email': '', 'Passwd': '', 'service': 'blogger', 'source': 'exampleCo-exampleApp-1.0'})
headers = {"Content-type": "application/x-www-form-urlencoded"}
conn = httplib.HTTPSConnection("www.google.com")
conn.request("POST","/accounts/ClientLogin",params,headers)
response = conn.getresponse()
print response.status
data = response.read()
conn.close()
print data

auth = re.search('Auth=(.*)$',data).group(0)
print auth


s = Template("""

$header
$payload

Koen Serry
http://www.blogger.com/profile/03836830737950982447
noreply@blogger.com

""")


f = open("blog.txt")
title = f.readline().rstrip()
content = " ".join(f.readlines())
params = s.substitute(header=title,payload=content)
headers = {"Authorization": "GoogleLogin auth="+auth,'Content-Type': 'application/atom+xml'}

conn = httplib.HTTPConnection("www.blogger.com")
conn.request("POST","/feeds/posts/default",params,headers)

response = conn.getresponse()
print response.status
data = response.read()
conn.close()
print data
```