---
id: applications-antivirus-kaspersky-snmp
title: Kaspersky
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Pack Assets

### Templates

The Centreon Plugin Pack **Kaspersky** brings a host template:

* App-Antivirus-Kaspersky-SNMP-custom-custom

It brings the following service templates:

| Service Alias   | Service Template                             | Service Description                                                     | Default |
|:----------------|:---------------------------------------------|:------------------------------------------------------------------------|:--------|
| Updates         | App-Antivirus-Kaspersky-Updates-SNMP         | Check delay since last server update and number of not up to date hosts | X       |
| Protection      | App-Antivirus-Kaspersky-Protection-SNMP      | Check protection status                                                 | X       |
| Logical-Network | App-Antivirus-Kaspersky-Logical-Network-SNMP | Check logical network status                                            | X       |
| Full-Scan       | App-Antivirus-Kaspersky-Full-Scan-SNMP       | Check full scan status                                                  | X       |
| Events          | App-Antivirus-Kaspersky-Events-SNMP          | Check events status                                                     | X       |
| Deployment      | App-Antivirus-Kaspersky-Deployment-SNMP      | Check deployment status                                                 | X       |


> **Default** services are automatically created when the host template is applied.

### Collected metrics & status

<Tabs groupId="sync">
<TabItem value="Deployment" label="Deployment">

| Metric Name                          | Unit  |
|:-------------------------------------|:------|
| status                               |       |
| hosts.antivirus.installed.count      | count |
| hosts.antivirus.install.failed.count | count |
| hosts.expiring.licence.count         | count |
| hosts.expired.licence.count          | count |

</TabItem>
<TabItem value="Events" label="Events">

| Metric Name           | Unit  |
|:----------------------|:------|
| status                |       |
| events.critical.count | count |

</TabItem>
<TabItem value="Full-Scan" label="Full-Scan">

| Metric Name           | Unit  |
|:----------------------|:------|
| status                |       |
| hosts.unscanned.count | count |

</TabItem>
<TabItem value="Logical-Network" label="Logical-Network">

| Metric Name              | Unit  |
|:-------------------------|:------|
| status                   |       |
| hosts.new.count          | count |
| groups.total.count       | count |
| hosts.notconnected.count | count |
| hosts.uncontrolled.count | count |

</TabItem>
<TabItem value="Protection" label="Protection">

| Metric Name                                        | Unit  |
|:---------------------------------------------------|:------|
| status                                             |       |
| protection.hosts.antivirus.notrunning.count        | count |
| protection.hosts.realtime.notrunning.count         | count |
| protection.hosts.realtime.unacceptable.level.count | count |
| protection.hosts.uncured.objects.count             | count |
| protection.hosts.toomanythreats.count              | count |

</TabItem>
<TabItem value="Updates" label="Updates">

| Metric Name                     | Unit  |
|:--------------------------------|:------|
| status                          |       |
| update.server.freshness.seconds | s     |
| update.hosts.outdated.count     | count |

</TabItem>
</Tabs>

## Prerequisites

### SNMP Configuration

To use this pack, the SNMP service must be properly configured on your ressource.
Please refer to the official documentation from XXX:
* LINK

### Network flow

The target server must be reachable from the Centreon poller on the UDP/161
SNMP port.

## Setup

### Monitoring Pack

If the platform uses an *online* license, you can skip the package installation
instruction below as it is not required to have the pack displayed within the
**Configuration > Plugin Packs > Manager** menu.
If the platform uses an *offline* license, install the package on the **central server**
with the command corresponding to the operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-applications-antivirus-kaspersky-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-applications-antivirus-kaspersky-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-antivirus-kaspersky-snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-applications-antivirus-kaspersky-snmp
```

</TabItem>
</Tabs>

Whatever the license type (*online* or *offline*), install the **Kaspersky** Pack through
the **Configuration > Plugin Packs > Manager** menu.

### Plugin

Since Centreon 22.04, you can benefit from the 'Automatic plugin installation' feature.
When this feature is enabled, you can skip the installation part below.

You still have to manually install the plugin on the poller(s) when:
- Automatic plugin installation is turned off
- You want to run a discovery job from a poller that doesn't monitor any resource of this kind yet

> More information in the [Installing the plugin](/docs/monitoring/pluginpacks/#installing-the-plugin) section.

Use the commands below according to your operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Applications-Antivirus-Kaspersky-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Applications-Antivirus-Kaspersky-Snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Antivirus-Kaspersky-Snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-applications-antivirus-kaspersky-snmp
```

</TabItem>
</Tabs>

## Configuration

### Host

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill the **Name**, **Alias** & **IP Address/DNS** fields according to your ressource settings.
3. Apply the **App-Antivirus-Kaspersky-SNMP-custom-custom** template to the host
4. Once the template is applied, fill in the corresponding macros. Some macros are mandatory.

| Mandatory      | Macro            | Description                                                                       | Default |
|:---------------|:-----------------|:----------------------------------------------------------------------------------|:--------|
|                | SNMPEXTRAOPTIONS | Any extra option you may want to add to every command line (eg. a --verbose flag) |         |

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`) and test the plugin by
running the following command:

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
	--mode=updates \
	--hostname=10.0.0.1 \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community'  \
	--warning-status='' \
	--critical-status='' \
	--warning-last-server-update='' \
	--critical-last-server-update='' \
	--warning-not-updated='' \
	--critical-not-updated='' \
	
```

The expected command output is shown below:

```bash
OK:    | 'update.server.freshness.seconds'=53s;;;0; 'update.hosts.outdated.count'=28;;;0 ; 
```

### Available modes

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
    --list-mode
```

The plugin brings the following modes:

| Mode            | Template                                     |
|:----------------|:---------------------------------------------|
| deployment      | App-Antivirus-Kaspersky-Deployment-SNMP      |
| events          | App-Antivirus-Kaspersky-Events-SNMP          |
| full-scan       | App-Antivirus-Kaspersky-Full-Scan-SNMP       |
| logical-network | App-Antivirus-Kaspersky-Logical-Network-SNMP |
| protection      | App-Antivirus-Kaspersky-Protection-SNMP      |
| updates         | App-Antivirus-Kaspersky-Updates-SNMP         |



### Available options

#### Global optionsAll global options are listed here:

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type   |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------|
| --mode                                     | Choose a mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Global |
| --dyn-mode                                 | Specify a mode with the path (separated by '::').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Global |
| --list-mode                                | List available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Global |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Global |
| --version                                  | Display plugin version.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Global |
| --pass-manager                             | Use a password manager.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Global |
| --verbose                                  | Display long output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Output |
| --debug                                    | Display also debug messages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output |
| --filter-perfdata                          | Filter perfdata that match the regexp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Output |
| --filter-perfdata-adv                      | Advanced perfdata filter.  Eg: --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Output |
| --explode-perfdata-max                     | Put max perfdata (if it exist) in a specific perfdata (without values: same with '\_max' suffix) (Multiple options)                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Output |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Change storage free perfdata in used:     --change-perfdata=free,used,invert()      Change storage free perfdata in used:     --change-perfdata=used,free,invert()      Scale traffic values automaticaly:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()   | Output |
| --extend-perfdata-group                    | Extend perfdata from multiple perfdatas (methods in target are: min, max, average, sum) Syntax: --extend-perfdata-group=searchlabel,newlabel,target\[,\[newuom\],\[m in\],\[max\]\]  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'                                               | Output |
| --change-short-output --change-long-output | Change short/long output display: --change-short-output=pattern~replace~modifier                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output |
| --change-exit                              | Change exit code: --change-exit=unknown=critical                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output |
| --range-perfdata                           | Change perfdata range thresholds display: 1 = start value equals to '0' is removed, 2 = threshold range is not display.                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Output |
| --filter-uom                               | Filter UOM that match the regexp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Output |
| --opt-exit                                 | Optional exit code for an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc) (Default: unknown).                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output |
| --output-ignore-perfdata                   | Remove perfdata from output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output |
| --output-ignore-label                      | Remove label status from output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output |
| --output-xml                               | Display output in XML format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Output |
| --output-json                              | Display output in JSON format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Output |
| --output-openmetrics                       | Display metrics in OpenMetrics format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Output |
| --output-file                              | Write output in file (can be used with json and xml options)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output |
| --disco-format                             | Display discovery arguments (if the mode manages it).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Output |
| --disco-show                               | Display discovery values (if the mode manages it).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Output |
| --float-precision                          | Set the float precision for thresholds (Default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Output |
| --source-encoding                          | Set encoding of monitoring sources (In some case. Default: 'UTF-8').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Output |
| --hostname                                 | Hostname to query (required).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Snmp   |
| --snmp-community                           | Read community (defaults to public).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Snmp   |
| --snmp-version                             | Version: 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Snmp   |
| --snmp-port                                | Port (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Snmp   |
| --snmp-timeout                             | Timeout in secondes (default: 1) before retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Snmp   |
| --snmp-retries                             | Set the number of retries (default: 5) before failure.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Snmp   |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Snmp   |
| --subsetleef                               | How many oid values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                   | Snmp   |
| --snmp-autoreduce                          | Auto reduce SNMP request size in case of SNMP errors (By default, the divisor is 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Snmp   |
| --snmp-force-getnext                       | Use snmp getnext function (even in snmp v2c and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Snmp   |
| --snmp-username                            | Security name (only for SNMP v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Snmp   |
| --authpassphrase                           | Authentication protocol pass phrase.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Snmp   |
| --authprotocol                             | Authentication protocol: MD5\|SHA. Since net-snmp 5.9.1: SHA224\|SHA256\|SHA384\|SHA512.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Snmp   |
| --privpassphrase                           | Privacy protocol pass phrase                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Snmp   |
| --privprotocol                             | Privacy protocol: DES\|AES. Since net-snmp 5.9.1: AES192\|AES192C\|AES256\|AES256C.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Snmp   |
| --contextname                              | Context name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Snmp   |
| --contextengineid                          | Context engine ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Snmp   |
| --securityengineid                         | Security engine ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Snmp   |
| --snmp-errors-exit                         | Exit code for SNMP Errors (default: unknown)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Snmp   |
| --snmp-tls-transport                       | TLS Transport communication used (can be: 'dtlsudp', 'tlstcp').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Snmp   |
| --snmp-tls-our-identity                    | Our X.509 identity to use, which should either be a fingerprint or the filename that holds the certificate.                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Snmp   |
| --snmp-tls-their-identity                  | The remote server's identity to connect to, specified as either a fingerprint or a file name. Either this must be specified, or the hostname below along with a trust anchor.                                                                                                                                                                                                                                                                                                                                                                                              | Snmp   |
| --snmp-tls-their-hostname                  | The remote server's hostname that is expected. If their certificate was signed by a CA then their hostname presented in the certificate must match this value or the connection fails to be established (to avoid man-in-the-middle attacks).                                                                                                                                                                                                                                                                                                                              | Snmp   |
| --snmp-tls-trust-cert                      | A trusted certificate to use as trust anchor (like a CA certificate) for verifying a remote server's certificate. If a CA certificate is used to validate a certificate then the TheirHostname parameter must also be specified to ensure their presented hostname in the certificate matches.                                                                                                                                                                                                                                                                             | Snmp   |


#### Modes options

All  modes specific options are listed here:

<Tabs groupId="sync">
<TabItem value="Deployment" label="Deployment">

| Option            | Description                                                                                                           | Type |
|:------------------|:----------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}     | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}   | Mode |
| --warning-*       | Threshold warning. Can be: 'progress' (counter or %), 'failed', 'expiring', 'expired'.                                | Mode |
| --critical-*      | Threshold critical. Can be: 'progress' (counter or %), 'failed', 'expiring', 'expired'.                               | Mode |
| --percent         | Set this option if you want to use percent on progress thresholds.                                                    | Mode |

</TabItem>
<TabItem value="Events" label="Events">

| Option            | Description                                                                                                           | Type |
|:------------------|:----------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}     | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}   | Mode |
| --warning-*       | Threshold warning. Can be: 'events'.                                                                                  | Mode |
| --critical-*      | Threshold critical. Can be: 'events'.                                                                                 | Mode |

</TabItem>
<TabItem value="Full-Scan" label="Full-Scan">

| Option            | Description                                                                                                           | Type |
|:------------------|:----------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}     | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}   | Mode |
| --warning-*       | Threshold warning. Can be: 'not-scanned'.                                                                             | Mode |
| --critical-*      | Threshold critical. Can be: 'not-scanned'.                                                                            | Mode |

</TabItem>
<TabItem value="Logical-Network" label="Logical-Network">

| Option            | Description                                                                                                           | Type |
|:------------------|:----------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}     | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}   | Mode |
| --warning-*       | Threshold warning. Can be: 'new-hosts', 'groups', 'not-connected-long-time', 'not-controlled'.                        | Mode |
| --critical-*      | Threshold critical. Can be: 'new-hosts', 'groups', 'not-connected-long-time', 'not-controlled'.                       | Mode |

</TabItem>
<TabItem value="Protection" label="Protection">

| Option            | Description                                                                                                                     | Type |
|:------------------|:--------------------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}               | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}             | Mode |
| --warning-*       | Threshold warning. Can be: 'no-antivirus', 'no-real-time', 'not-acceptable-level', 'not-cured-objects', 'too-many-threats'.     | Mode |
| --critical-*      | Threshold critical. Can be: 'no-antivirus', 'no-real-time', 'not-acceptable-level', 'not-cured-objects', 'too-many-threats'.    | Mode |

</TabItem>
<TabItem value="Updates" label="Updates">

| Option            | Description                                                                                                           | Type |
|:------------------|:----------------------------------------------------------------------------------------------------------------------|:-----|
| --warning-status  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}     | Mode |
| --critical-status | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status}   | Mode |
| --warning-*       | Threshold warning. Can be: 'last-server-update', 'not-updated'.                                                       | Mode |
| --critical-*      | Threshold critical. Can be: 'last-server-update', 'not-updated'.                                                      | Mode |
| --timezone        | Timezone options. Default is 'GMT'.                                                                                   | Mode |

</TabItem>
</Tabs>


All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
	--mode=updates \
    --help
```

### Troubleshooting

Please find the [troubleshooting documentation](../getting-started/how-to-guides/troubleshooting-plugins.md)
for Centreon Plugins typical issues.