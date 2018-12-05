# SFDX App

This repo demonstrates an issue with Salesforce DX observed in Winter '19
and API 44.0, regarding the installation of Salesforce CPQ in new scratch orgs.

Specifically, `force:source:push` fails with the error message,
"Required field is missing: activateRSS".

## Dev, Build and Test

1. Clone this repo
2. Create a new scratch org using **config/project-scratch-def.json**
3. Push source to the new scratch org using `sfdx force:source:push`

At this point you will see the error below, which prevents the package
from actually being installed in the org.

```txt
PROJECT PATH                                                             ERROR
───────────────────────────────────────────────────────────────────────  ──────────────────────────────────────
force-app/main/default/installedPackages/SBQQ.installedPackage-meta.xml  Required field is missing: activateRSS
```

## Workaround

Edit the **SBQQ.installedPackage-meta.xml** file. First, delete the line below.

```xml
    <activateRSS xsi:nil="true"/>
```

Then put the following line in the same place.

```xml
    <activateRSS>false</activateRSS>
```

## Resources

* "[Push Source to the Scratch Org][1]." _Salesforce DX Developer Guide_.

[1]: https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_push_md_to_scratch_org.htm
