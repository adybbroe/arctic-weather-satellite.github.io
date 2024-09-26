---
layout: page
title: Real-time data
---

## Example - how to fetch data

To download Arctic Weather Satellite data from the three Nordic S3 buckets you will need to get access/secret key pairs, one pair of keys for each bucket. Also, of couse you need to know the URLs and the bucket names. For all that, please contact us at: <a href="assets/img/email_image.png"><img src="assets/img/email_image.png" alt="Contact us at email address" height="20"/></a>


Below is an example of how to fetch the latest Level-1c data from the bucket at SMHI (data received at Kangerlussuaq, Greenland) from a Linux terminal.

First set environment variables for the keys:

{% highlight bash %}

export SMHI_RO_AWS_ACCESS="<the access key you get from us>"
export SMHI_RO_AWS_SECRET="<the secret key you get from us>"

{% endhighlight %}

Then after adapting the path to where you store the AWS data locally you can run the python code below, you can run the python code below to download the last 6 hours of level-1c data from the Kangerlussuaq station:

{% highlight python %}

import os
import s3fs
from pathlib import Path
from trollsift import Parser
from datetime import datetime, timedelta

PATTERN = "W_XX-{centre:s}-{station:s},SAT,{satname:s}-{sensor:s}-{level:s}-RAD_C_{centre:s}_{processing_time:%Y%m%d%H%M%S}_G_D_{starttime:%Y%m%d%H%M%S}_{endtime:%Y%m%d%H%M%S}_T_B____.nc"

awsat_local_dir = '/some/path/to/my/local/aws/data/' # Please adapt to the choice of your own

s3 = s3fs.S3FileSystem(client_kwargs={
    'endpoint_url': 'https://satobjectstore.smhi.se/'},
                       anon=False,
                       key=os.environ["SMHI_RO_AWS_ACCESS"],
                       secret=os.environ["SMHI_RO_AWS_SECRET"])

all_esa_l1c_files = s3.ls('satellite-data-kangerlussuaq-arctic-weather-satellite/awsat/l1c/esa')

p__ = Parser(PATTERN)

now = datetime(2024, 1, 15, 12, 0)
tdelta = timedelta(hours=6) # Last six hours of data

for awsatfile_str in all_esa_l1c_files:
    awsatfile = Path(awsatfile_str)
    localpath = Path(awsat_local_dir) / awsatfile.name
    res = p__.parse(awsatfile.name)
    obstime = res['starttime']
    if (now - obstime) < tdelta:
        s3.get(awsatfile_str, str(localpath))

{% endhighlight %}
