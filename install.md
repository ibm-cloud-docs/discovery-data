---

copyright:
  years: 2019, 2024
lastupdated: "2024-10-03"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Installation overview
{: #install}

Find information about how to install {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d}

This information applies only to installed deployments.
{: note}

## Full installation instructions
{: #full-installation-instructions}

- [5.0.0](https://www.ibm.com/docs/SSQNUZ_5.0.x/svc-discovery/discovery-install-overview.html){: external}
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

| {{site.data.keyword.discoveryshort}} version | {{site.data.keyword.icp4dfull_notm}} version | Red Hat OpenShift version |
| ----------------------------------|----------------|----------------|
| 5.0.3 | 5.0.x | 4.16 |
| 5.0.3 | 5.0.x | 4.15 |
| 5.0.3 | 5.0.x | 4.14 |
| 5.0.3 | 5.0.x | 4.12 |
| 5.0.1 | 5.0.1 | 4.15 |
| 5.0.1 | 5.0.1 | 4.14 |
| 5.0.1 | 5.0.1 | 4.12 |
| 5.0.0 | 5.0.0 | 4.15 |
| 5.0.0 | 5.0.0 | 4.14 |
| 5.0.0 | 5.0.0 | 4.12 |
| 4.8.6 | 4.8.6 | 4.15 |
| 4.8.6 | 4.8.6 | 4.14 |
| 4.8.6 | 4.8.6 | 4.12 |
| 4.8.5 | 4.8.5 | 4.15 |
| 4.8.5 | 4.8.5 | 4.14 |
| 4.8.5 | 4.8.5 | 4.12 |
| 4.8.4 | 4.8.4 | 4.14 |
| 4.8.4 | 4.8.4 | 4.12 |
| 4.8.3 | 4.8.3 | 4.14 |
| 4.8.3 | 4.8.3 | 4.12 |
| 4.8.2 | 4.8.2 | 4.14 |
| 4.8.2 | 4.8.2 | 4.12 |
| 4.8.0 | 4.8.1 | 4.14 |
| 4.8.0 | 4.8.1 | 4.12 |
| 4.8.0 | 4.8.0 | 4.12 |
| 4.7.3 | 4.7.3 | 4.12 |
| 4.7.3 | 4.7.3 | 4.10 |
| 4.7.1 | 4.7.1 | 4.12 |
| 4.7.1 | 4.7.1 | 4.10 |
| 4.7.0 | 4.7.0 | 4.12 |
| 4.7.0 | 4.7.0 | 4.10 |
| 4.6.5 | 4.6.6 | 4.12 |
| 4.6.5 | 4.6.6 | 4.10 |
| 4.6.5 | 4.6.5 | 4.12 |
| 4.6.5 | 4.6.5 | 4.10 |
| 4.6.3 | 4.6.4 | 4.12 |
| 4.6.3 | 4.6.4 | 4.10 |
| 4.6.3 | 4.6.3 | 4.10 |
| 4.6.2 | 4.6.2 | 4.10 |
| 4.6.2 | 4.6.2 | 4.8 |
| 4.6.2 | 4.6.1 | 4.10 |
| 4.6.2 | 4.6.1 | 4.8 |
| 4.6.0 | 4.6.0 | 4.10 |
| 4.6.0 | 4.6.0 | 4.8 |
| 4.5.3 | 4.5.3 | 4.10 |
| 4.5.3 | 4.5.3 | 4.8 |
| 4.5.3 | 4.5.3 | 4.6.29 or later |
| 4.5.1 | 4.5.2 | 4.10 |
| 4.5.1 | 4.5.2 | 4.8 |
| 4.5.1 | 4.5.2 | 4.6.29 or later |
| 4.5.1 | 4.5.1 | 4.10 |
| 4.5.1 | 4.5.1 | 4.8 |
| 4.5.1 | 4.5.1 | 4.6.29 or later |
| 4.5.0 | 4.5.0 | 4.10 |
| 4.5.0 | 4.5.0 | 4.8 |
| 4.5.0 | 4.5.0 | 4.6.29 or later |
| 4.0.9 | 4.0.9 | 4.8 |
| 4.0.9 | 4.0.9 | 4.6.29 or later |
| 4.0.8 | 4.0.8 | 4.8 |
| 4.0.8 | 4.0.8 | 4.6.29 or later |
| 4.0.7 | 4.0.7 | 4.8 |
| 4.0.7 | 4.0.7 | 4.6.29 or later |
| 4.0.6 | 4.0.6 | 4.8 |
| 4.0.6 | 4.0.6 | 4.6.29 or later |
| 4.0.5 | 4.0.5 | 4.8 |
| 4.0.5 | 4.0.5 | 4.6.29 or later |
| 4.0.4 | 4.0.4 | 4.8 |
| 4.0.4 | 4.0.4 | 4.6.29 or later |
| 4.0.3 | 4.0.3 | 4.8 |
| 4.0.3 | 4.0.3 | 4.6.29 or later |
| 4.0.2 | 4.0.2 | 4.8 |
| 4.0.2 | 4.0.2 | 4.6 |
| 4.0.0 | 4.0.0 | 4.6 |
| 2.2.1 | 3.5.0 | 4.5, 4.6 |
| 2.2.1 | 3.5.0 | 3.11.188 |
| 2.2.1 | 3.0.1 | 4.5, 4.6 |
| 2.2.1 | 3.0.1 | 3.11.188 |
| 2.2.0 | 3.5.0 | 4.5 |
| 2.2.0 | 3.5.0 | 3.11.188 |
| 2.2.0 | 3.0.1 | 4.5 |
| 2.2.0 | 3.0.1 | 3.11 |
| 2.1.4 | 3.0.1 | 3.11.188 |
| 2.1.4 | 2.5 | 3.11 |
| 2.1.3 | 3.0.1 | 3.11.188 |
| 2.1.3 | 2.5 | 3.11 |
{: caption="Support matrix" caption-side="top"}

The `3.11.188` version more precisely means 3.11.188 or a later 3.11 version.
