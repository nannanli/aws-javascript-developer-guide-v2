# Uploading an Archive to Amazon Glacier<a name="glacier-example-uploadrchive"></a>

![\[JavaScript code example that applies to Node.js execution\]](http://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/images/nodeicon.png)

**This Node\.js code example shows:**
+ How to upload an archive to Amazon Glacier using the `uploadArchive` method of the Amazon Glacier service object\.

The following example uploads a single `Buffer` object as an entire archive using the `uploadArchive` method of the Amazon Glacier service object\.

The example assumes you've already created a vault named `YOUR_VAULT_NAME`\. The SDK automatically computes the tree hash checksum for the data uploaded, though you can override it by passing your own checksum parameter:

## Prerequisite Tasks<a name="glacier-example-uploadrchive-prerequisites"></a>

To set up and run this example, you must first complete these tasks:
+ Install Node\.js\. For more information about installing Node\.js, see the [Node\.js website](https://nodejs.org)\.
+ Create a shared configurations file with your user credentials\. For more information about providing a shared credentials file, see [Loading Credentials in Node\.js from the Shared Credentials File](loading-node-credentials-shared.md)\.

## Configuring the SDK<a name="glacier-example-uploadrchive-configure-sdk"></a>

Configure the SDK for JavaScript by creating a global configuration object then setting the region for your code\. In this example, the region is set to `us-west-2`\.

```
// Load the SDK for JavaScript
var AWS = require('aws-sdk');
// Set the region 
AWS.config.update({region: 'us-west-2'});
```

## Upload the Archive<a name="glacier-example-uploadrchive-code"></a>

```
// Load the SDK for JavaScript
var AWS = require('aws-sdk');
// Set the region 
AWS.config.update({region: 'us-west-2'});
            
var glacier = new AWS.Glacier({apiVersion: '2012-06-01'}),
buffer = new Buffer(2.5 * 1024 * 1024); // 2.5MB buffer

var params = {vaultName: 'YOUR_VAULT_NAME', body: buffer};
glacier.uploadArchive(params, function(err, data) {
if (err) console.log("Error uploading archive!", err);
else console.log("Archive ID", data.archiveId);
});
```