---
ref: xu-amazon-aws-s3-02
layout: page
title: Connection
description: Connection
product: xtract-universal
parent: amazon-aws-s3
permalink: /:collection/:path
weight: 2
lang: en_GB
old_url: /Xtract-Universal-EN/default.aspx?pageid=connection5
---


The following settings can be made when setting up an AWS S3 connection. 

![XU_S3_DestinationDetails](/img/content/XU_S3_DestinationDetails.jpg){:class="img-responsive"}

**Access key ID and Secret key**<br>
This is how you authenticate against Amazon AWS. You can determine these values via AWS Identiy and Access Managment ([IAM](https://console.aws.amazon.com/iam/home#/home)).
Please see [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for further information.

**Connect**<br>
After entering Access key ID and Secret key, click on the Connect button. After successfully connecting you can select bucket name and region.

**Bucket name and Region**<br>
Select a bucket and a region this bucket is located in. The SAP data will be extracted into this bucket.
ATTENTION: The drop down menus list all available buckets and regions so you won't be prevented from selecting a wrong combination of bucket/region. Please validate the connectivity to the selected bucket by clicking on the the "Test Connection" button.

**Test Connection**<br>
Validates the right combination of bucket and region. Validates that the bucket is reachable from Xtract Universal using the entered access keys.

**Server-side encryption**<br>
Encrypts the data after the data has been uploaded to S3.<br>
NOTE: This is no transport encyption between Xtract Universal and S3. 

- **None**<br>
Sever sided encryption of data not active.

- **SSE-S3**<br>
Encrypts data using the by default available S3 user account encryptiong key ([S3 Managed Encryption Keys](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)).

- **SSE-KMS und Key ID**<br>
Encryption using a custom encrpytion key created on AWS ([AWS Key Management Services](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)). You can create the key from [here](https://console.aws.amazon.com/iam/home#/encryptionKeys/.)


**CSV Settings:**<br>
The settings in the tab CSV Settings correspond to the ones in the general [http-csv settings](../csv-via-http).
	
![XU_S3_DestinationDetails2](/img/content/XU_S3_DestinationDetails2.jpg){:class="img-responsive"}