---

copyright:
  years:  2018, 2023
lastupdated: "2023-03-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# About agent versions
{: #agent_version}

The {{site.data.keyword.mon_full_notm}} agent version consists of multiple parts:

```text
X.Y.Z
```
{: codeblock}

Where

- `X` represents the major version of an image.
- `Y` represents the minor version of an image.
- `Z` represents an incremental ID that determines the latest patched minor version.

For more information about the agent new features and new versions, see [Sysdig Agent Release Notes](https://docs.sysdig.com/en/docs/release-notes/sysdig-agent-release-notes/){: external}.

## End of support
{: #agent_version_eos}

The {{site.data.keyword.mon_full_notm}} service supports `n-3` versions back based on the minor number.
{: note}

## Deprecation
{: #agent_version_deprecation}

When an agent version becomes unsupported, the agent version is maintained for vulnerabilities for 3 years. After 3 years, the image is deprecated and unavailable.

Unsupported versions of the {{site.data.keyword.mon_full_notm}} agent have a 3-year deprecation policy.
{: note}
