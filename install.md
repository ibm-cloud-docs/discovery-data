---

copyright:
  years: 2019, 2025
lastupdated: "2025-07-14"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Installation overview
{: #install}

Find information about how to install {{site.data.keyword.discoveryfull}}.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

This information applies only to installed deployments.
{: note}

## Full installation instructions
{: #full-installation-instructions}

- [5.2.0](https://www.ibm.com/docs/SSNFH6_5.2.x/svc-discovery/discovery-install-overview.html){: external}
- [5.1.x](https://www.ibm.com/docs/SSNFH6_5.1.x/svc-discovery/discovery-install-overview.html){: external}
- [5.0.x](https://www.ibm.com/docs/SSQNUZ_5.0.x/svc-discovery/discovery-install-overview.html){: external}
- [4.8.x](https://www.ibm.com/docs/SSQNUZ_4.8.x/svc-discovery/discovery-install-overview.html){: external}
- [4.7.x](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-discovery/discovery-install-overview.html){: external}
- [4.6.x](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-install-overview.html){: external}
- [4.5.x](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-discovery/discovery-install-overview.html){: external}
- [4.0.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-installing-watson){: external}
- [2.2.0, 2.2.1](https://www.ibm.com/docs/cloud-paks/cp-data/3.5.0?topic=services-watson-discovery){: external}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019. {{site.data.keyword.discoveryfull}} is FISMA High Ready.

## Support matrix
{: #support-matrix}

You install {{site.data.keyword.icp4dfull_notm}}, and then install the {{site.data.keyword.discoveryshort}} service.

- The 4.6.2 release is the last supported release on Red Hat OpenShift Container Platform 4.8.
- The 4.5.3 release is the last supported release on Red Hat OpenShift Container Platform 4.6.29 or later.

### IBM Software Hub - Support matrix
{: #support-matrix-swh}

The following table describes which versions of {{site.data.keyword.discoveryshort}} are supported on which versions of IBM Software Hub and Red Hat OpenShift.

| {{site.data.keyword.discoveryshort}} version | IBM Software Hub version | Red Hat OpenShift version |
| ----------------------------------|----------------|----------------|
| 5.2.0 | 5.2.0 | 4.12, 4.14, 4.15, 4.16, 4.17, 4.18 |
| 5.1.2 | 5.1.3 | 4.12, 4.14, 4.15, 4.16, 4.17, 4.18 |
| 5.1.2 | 5.1.2 | 4.12, 4.14, 4.15, 4.16, 4.17 |
| 5.1.1 | 5.1.1 | 4.12, 4.14, 4.15, 4.16, 4.17 |
| 5.1.0 | 5.1.0 | 4.12, 4.14, 4.15, 4.16, 4.17 |
{: caption="IBM Software Hub - Support matrix" caption-side="top"}

For more information, see the supported [Red Hat OpenShift Container Platform versions](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=requirements-software#platform__ocp__title__1){: external}. 

### {{site.data.keyword.icp4dfull_notm}} - Support matrix
{: #support-matrix-cpd}

The following table describes which versions of {{site.data.keyword.discovery-data_short}} are supported on which versions of {{site.data.keyword.icp4dfull_notm}} and Red Hat OpenShift.

| {{site.data.keyword.discoveryshort}} version | {{site.data.keyword.icp4dfull_notm}} version | Red Hat OpenShift version |
| ----------------------------------|----------------|----------------|
| 5.0.3 | 5.0.3 | 4.12, 4.14, 4.15, 4.16 |
| 5.0.1 | 5.0.1, 5.0.2 | 4.12, 4.14, 4.15 |
| 5.0.0 | 5.0.0 | 4.12, 4.14, 4.15 |
| 4.8.9 | Same version as {{site.data.keyword.discovery-data_short}} | 4.12, 4.14, 4.15, 4.16, 4.18 |
| 4.8.7, 4.8.8 | Same version as {{site.data.keyword.discovery-data_short}} | 4.12, 4.14, 4.15, 4.16 |
| 4.8.5, 4.8.6 | Same version as {{site.data.keyword.discovery-data_short}} | 4.12, 4.14, 4.15 |
| 4.8.2, 4.8.3, 4.8.4 | Same version as {{site.data.keyword.discovery-data_short}} | 4.12, 4.14 |
| 4.8.0 | 4.8.1 | 4.12, 4.14 |
| 4.8.0 | 4.8.0 | 4.12 |
| 4.7.3 | 4.7.3, 4.7.4 | 4.10, 4.12 |
| 4.7.1 | 4.7.1, 4.7.2 | 4.10, 4.12 |
| 4.7.0 | 4.7.0 | 4.10, 4.12 |
| 4.6.5 | 4.6.5, 4.6.6 | 4.10, 4.12 |
| 4.6.3 | 4.6.4 | 4.10, 4.12 |
| 4.6.3 | 4.6.3 | 4.10 |
| 4.6.2 | 4.6.2 | 4.8, 4.10 |
| 4.6.0 | 4.6.0, 4.6.1 | 4.8, 4.10 |
| 4.5.3 | 4.5.3 | 4.6.29 or later, 4.8, 4.10 |
| 4.5.1 | 4.5.1, 4.5.2 | 4.6.29 or later, 4.8, 4.10 |
| 4.5.0 | 4.5.0 | 4.6.29 or later, 4.8, 4.10 |
| 4.0.3, 4.0.4, 4.0.5, 4.0.6, 4.0.7, 4.0.8, 4.0.9 | Same version as {{site.data.keyword.discovery-data_short}} | 4.6.29 or later, 4.8 |
| 4.0.2 | 4.0.2 | 4.6, 4.8 |
| 4.0.0 | 4.0.0, 4.0.1 | 4.6 |
{: caption="IBM Cloud Pak for Data - Support matrix" caption-side="top"}

For more information, see the supported [Red Hat OpenShift Container Platform versions](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=requirements-software#software-reqs__platform__title__1){: external}. 
