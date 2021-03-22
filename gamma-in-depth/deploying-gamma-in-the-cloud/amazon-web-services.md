---
description: Setup Gamma Server on AWS
---

# Amazon Web Services

1. Log into your amazon management console
2. Select your desired region
3. select EC2 -&gt; Instances -&gt; Launch Instances
4. Navigate to "_AWS Marketplace_” and enter “_Orbs_” in the search text box
5. Select "_Orbs Network Developer Kit_” -&gt; Continue -&gt; Review and launch \(or edit instance parameters\)
6. To finalize the AMI initialization: 

   * Click Launch
   * Select your desired option for ssh key pair. No key pair is required. But you may choose to set one up.
   * Launch instance

   A new instance is now launching. 

7. To obtain your server host name or IP address, navigate to EC2 instances console 

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

