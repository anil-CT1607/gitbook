# E-Invoicing FTP Magnet

![](../.gitbook/assets/ftp-magnet-banner.png)

FTP Magnet is a middleware application between your FTP server and ClearTax E-Invoicing application. You can export data from your ERP to your own FTP server. As a part of on-boarding, ClearTax configures it’s FTP Magnet to connect to your FTP server. The FTP Magnet reads the input files from your FTP server and uploads them to ClearTax E-Invoicing application. Once the uploaded files are processed, it writes the response back to your FTP server.

## Downloads

**Specification document and a typical project plan**:

{% file src="../.gitbook/assets/einv-ftp-magnet-specification-document-and-project-plan-v1.0.pdf" %}

**Sample Processing Success File:**

{% file src="../.gitbook/assets/einv-sftp-sample-processing-success-file.xlsx.csv" %}

**Sample Processing Failure Error File:**

{% file src="../.gitbook/assets/einv-sftp-sample-processing-failure-error-file.xlsx.csv" %}

{% hint style="info" %}
The success and error file templates are subject to change. We recommend you to map the output with flexible options to add or change the headers in the future.
{% endhint %}

