---
description: Setup Gamma Server on GCP
---

# Google Cloud Platform

1. Go to your GCP console at: [https://console.cloud.google.com/home/dashboard](https://console.cloud.google.com/home/dashboard)
2. Open the hamburger menu on the left side
3.  Choose "_Marketplace_"
4. Under the "_Search for solutions_" text box type "_Orbs_" and choose the result "_orbs-gamma-devkit_"
5.  Click on "_Launch_"
6. If you want to change any parameters of the VM  please do so in this step
7. Click on "_Deploy_"
8. The public IP address of the newly created machine will appear on this page under the property titled "_Site address_": ![Screen Shot 2021-03-09 at 16.18.10.png](https://mail.google.com/mail/u/0?ui=2&ik=396b6a8279&attid=0.1&permmsgid=msg-f:1693771032118519606&th=17817bc79c456736&view=fimg&sz=s0-l75-ft&attbid=ANGjdJ8C_ptV1jmJ28uZlPjK9O369GQU4wfSsDF65nnx2fbRa3h5FkIqRIDC3VQHqFjdQ6AbL-2Rr1_HxncoV-JQWgkOSrXqVLcbaWWz1sLMstrXqanNSMKN2ncspMQ&disp=emb&realattid=ii_km23m2cc0)

You may now work with gamma server remotely. For more information on setting up a remote gamma environment on your local dev machine,  [click here](../working-with-multiple-environments.md#gamma-config-json)

{% code title="orbs-gamma-config.json" %}
```text
{
  "Environments": {
    "staging": {
      "VirtualChain": 42,
      "Endpoints": ["http://<ip>:8080"]
    }
  }
}
```
{% endcode %}

Prism block explorer will be available at `http://<ip>:3000/`

After setting up your Gamma remote environment, you can deploy your may [deploy first contract](../../getting-started/deploying-your-first-contract.md)

