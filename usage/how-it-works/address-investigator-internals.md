---
description: Behind the scenes...
---

# 📬 Address Investigator Internals

`GetIspConfig`, once called with the e-mail address, processes the address and builds the XML string. Then, it proceeds to generate the URL based on the host name and downloads the XML from the ISP database.

Once downloaded, the resulting XML file is then deserialized to a new instance of the `ClientConfig` class, installing the values to the class instance.

To take a look at the ClientConfig structure, refer to the below link.

{% embed url="https://aptivi.github.io/Addresstigator/api/Addresstigator.ClientConfig.html" %}
