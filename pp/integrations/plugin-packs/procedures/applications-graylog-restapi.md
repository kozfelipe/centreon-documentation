---
id: applications-graylog-restapi
title: Graylog
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Pack Assets

### Templates

The Centreon Plugin Pack **Graylog** brings a host template:

* App-Graylog-Restapi-custom-custom

It brings the following service templates:

| Service Alias        | Service Template                  | Service Description                                         | Default |
|:---------------------|:----------------------------------|:------------------------------------------------------------|:--------|
| Query                | App-Graylog-Query-Restapi         | Check Lucene query matches on a Graylog server via Rest Api |         |
| System-Notifications | App-Graylog-Notifications-Restapi | Check Graylog server system notifications via Rest Api      | X       |

> **Default** services are automatically created when the host template is applied.


### Collected metrics & status

<Tabs groupId="sync">
<TabItem value="Query" label="Query">

| Metric Name               | Unit  |
|:--------------------------|:------|
| graylog.query.match.count | count |

</TabItem>
<TabItem value="System-Notifications" label="System-Notifications">

| Metric Name                               | Unit  |
|:------------------------------------------|:------|
| graylog.system.notifications.total.count  | count |
| graylog.system.notifications.normal.count | count |
| graylog.system.notifications.urgent.count | count |

</TabItem>
</Tabs>

## Prerequisites

*Specify prerequisites that are relevant. You may want to just provide a link
to the manufacturer official documentation BUT you should try to be as complete
as possible here as it will save time to everybody.*

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
dnf install centreon-pack-applications-graylog-restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-applications-graylog-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-graylog-restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-applications-graylog-restapi
```

</TabItem>
</Tabs>

Whatever the license type (*online* or *offline*), install the **Graylog** Pack through
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
dnf install centreon-plugin-Applications-Graylog-Restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Applications-Graylog-Restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Graylog-Restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-applications-graylog-restapi
```

</TabItem>
</Tabs>

## Configuration

### Host

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill the **Name**, **Alias** & **IP Address/DNS** fields according to your ressource settings.
3. Apply the **App-Graylog-Restapi-custom-custom** template to the host
4. Once the template is applied, fill in the corresponding macros. Some macros are mandatory.

| Mandatory      | Macro        | Description                                                                       | Default |
|:---------------|:-------------|:----------------------------------------------------------------------------------|:--------|
|                | APIPASSWORD  |                                                                                   |         |
|                | APIPORT      | API port                                                                          | 9000    |
|                | APIPROTOCOL  | Specify https if needed                                                           | http    |
|                | APIUSERNAME  |                                                                                   |         |
|                | EXTRAOPTIONS | Any extra option you may want to add to every command line (eg. a --verbose flag) |         |

### Service

<Tabs groupId="sync">
<TabItem value="Query" label="Query">

| Mandatory      | Macro                | Description                                                  | Default |
|:---------------|:---------------------|:-------------------------------------------------------------|:--------|
|                | TIMEFRAME            | Set timeframe in seconds (E.g '300' to check last 5 minutes) | 300     |
|                | QUERY                | Set a Lucene query                                           |         |
|                | WARNINGQUERYMATCHES  |                                                              |         |
|                | CRITICALQUERYMATCHES |                                                              |         |

</TabItem>
<TabItem value="System-Notifications" label="System-Notifications">

| Mandatory      | Macro                       | Description                                                                                             | Default |
|:---------------|:----------------------------|:--------------------------------------------------------------------------------------------------------|:--------|
|                | FILTERSEVERITY              | Filter on specific notification severity. Can be 'normal' or 'urgent'. (Default: both severities shown) |         |
|                | FILTERNODE                  | Filter notifications by node ID. (Default: all notifications shown)                                     |         |
|                | WARNINGNOTIFICATIONSTOTAL   |                                                                                                         |         |
|                | CRITICALNOTIFICATIONSTOTAL  |                                                                                                         |         |
|                | WARNINGNOTIFICATIONSNORMAL  |                                                                                                         |         |
|                | CRITICALNOTIFICATIONSNORMAL |                                                                                                         |         |
|                | WARNINGNOTIFICATIONSURGENT  |                                                                                                         |         |
|                | CRITICALNOTIFICATIONSURGENT |                                                                                                         |         |

</TabItem>
</Tabs>

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`) and test the plugin by
running the following command:

```bash
/usr/lib/centreon/plugins//centreon_graylog_restapi.pl \
	--plugin=apps::graylog::restapi::plugin \
	--mode=query \
	--hostname='10.0.0.1' \
	--port='' \
	--proto='' \
	--api-username='' \
	--api-password=''  \
	--query='' \
	--timeframe='' \
	--warning-query-matches='' \
	--critical-query-matches='' \
	
```

The expected command output is shown below:

```bash
OK:  | 'graylog.query.match.count'=34;;;0 ;;;;;  
```

### Available modes

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins//centreon_graylog_restapi.pl \
	--plugin=apps::graylog::restapi::plugin \
    --list-mode
```

The plugin brings the following modes:

| Mode          | Linked service template           |
|:--------------|:----------------------------------|
| notifications | App-Graylog-Notifications-Restapi |
| query         | App-Graylog-Query-Restapi         |



### Available options

#### Global optionsAll global options are listed here:

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type         |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------|
| --mode                                     | Choose a mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Global       |
| --dyn-mode                                 | Specify a mode with the path (separated by '::').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Global       |
| --list-mode                                | List available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Global       |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Global       |
| --version                                  | Display plugin version.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Global       |
| --custommode                               | Choose a custom mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Global       |
| --list-custommode                          | List available custom modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Global       |
| --multiple                                 | Multiple custom mode objects (required by some specific modes)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Global       |
| --pass-manager                             | Use a password manager.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Global       |
| --verbose                                  | Display long output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Output       |
| --debug                                    | Display also debug messages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output       |
| --filter-perfdata                          | Filter perfdata that match the regexp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Output       |
| --filter-perfdata-adv                      | Advanced perfdata filter.  Eg: --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Output       |
| --explode-perfdata-max                     | Put max perfdata (if it exist) in a specific perfdata (without values: same with '\_max' suffix) (Multiple options)                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Output       |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Change storage free perfdata in used:     --change-perfdata=free,used,invert()      Change storage free perfdata in used:     --change-perfdata=used,free,invert()      Scale traffic values automaticaly:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()   | Output       |
| --extend-perfdata-group                    | Extend perfdata from multiple perfdatas (methods in target are: min, max, average, sum) Syntax: --extend-perfdata-group=searchlabel,newlabel,target\[,\[newuom\],\[m in\],\[max\]\]  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'                                               | Output       |
| --change-short-output --change-long-output | Change short/long output display: --change-short-output=pattern~replace~modifier                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output       |
| --change-exit                              | Change exit code: --change-exit=unknown=critical                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output       |
| --range-perfdata                           | Change perfdata range thresholds display: 1 = start value equals to '0' is removed, 2 = threshold range is not display.                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Output       |
| --filter-uom                               | Filter UOM that match the regexp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Output       |
| --opt-exit                                 | Optional exit code for an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc) (Default: unknown).                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output       |
| --output-ignore-perfdata                   | Remove perfdata from output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output       |
| --output-ignore-label                      | Remove label status from output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Output       |
| --output-xml                               | Display output in XML format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Output       |
| --output-json                              | Display output in JSON format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Output       |
| --output-openmetrics                       | Display metrics in OpenMetrics format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Output       |
| --output-file                              | Write output in file (can be used with json and xml options)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Output       |
| --disco-format                             | Display discovery arguments (if the mode manages it).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Output       |
| --disco-show                               | Display discovery values (if the mode manages it).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Output       |
| --float-precision                          | Set the float precision for thresholds (Default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Output       |
| --source-encoding                          | Set encoding of monitoring sources (In some case. Default: 'UTF-8').      Graylog Rest API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Output       |
| --hostname                                 | Graylog hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Api          |
| --url-path                                 | API url path (Default: '/api/')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Api          |
| --port                                     | API port (Default: 9000)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Api          |
| --proto                                    | Specify https if needed (Default: 'http')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Api          |
| --username                                 | Specify username for authentication (Mandatory if --credentials is specified)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Api          |
| --password                                 | Specify password for authentication (Mandatory if --credentials is specified)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Api          |
| --timeout                                  | Set HTTP timeout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Api          |
| --requested-by                             | Set request HTTP header (Default: 'cli')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Api          |
| --http-peer-addr                           | Set the address you want to connect (Useful if hostname is only a vhost. no ip resolve)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Http global  |
| --proxyurl                                 | Proxy URL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Http global  |
| --proxypac                                 | Proxy pac file (can be an url or local file)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Http global  |
| --insecure                                 | Insecure SSL connections.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Http global  |
| --http-backend                             | Set the backend used (Default: 'lwp') For curl: --http-backend=curl                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Http global  |
| --ssl-opt                                  | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Backend lwp  |
| --ssl                                      | Set SSL version (=TLSv1).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Backend lwp  |
| --curl-opt                                 | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                                                                                                                                                                                                                                                                                                                                                           | Backend curl |
| --memcached                                | Memcached server to use (only one server).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Retention    |
| --redis-server                             | Redis server to use (only one server). SYntax: address\[:port\]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Retention    |
| --redis-attribute                          | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Retention    |
| --redis-db                                 | Set Redis database index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Retention    |
| --failback-file                            | Failback on a local file if redis connection failed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Retention    |
| --memexpiration                            | Time to keep data in seconds (Default: 86400).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Retention    |
| --statefile-dir                            | Directory for statefile (Default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Retention    |
| --statefile-suffix                         | Add a suffix for the statefile name (Default: '').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Retention    |
| --statefile-concat-cwd                     | Concat current working directory with option '--statefile-dir'. Useful on Windows when plugin is compiled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Retention    |
| --statefile-format                         | Format used to store cache (can be: 'dumper', 'storable', 'json').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Retention    |
| --statefile-key                            | Key to encrypt/decrypt cache.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Retention    |
| --statefile-cipher                         | Cipher to encrypt cache (Default: 'AES').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Retention    |


#### Modes options

All  modes specific options are listed here:

<Tabs groupId="sync">
<TabItem value="Query" label="Query">

| Option                                           | Description                                                     | Type |
|:-------------------------------------------------|:----------------------------------------------------------------|:-----|
| --query                                          | Set a Lucene query.                                             | Mode |
| --timeframe                                      | Set timeframe in seconds (E.g '300' to check last 5 minutes).   | Mode |
| --warning-query-matches --critical-query-matches | Threshold on the number of results.                             | Mode |

</TabItem>
<TabItem value="System-Notifications" label="System-Notifications">

| Option                     | Description                                                                                                     | Type |
|:---------------------------|:----------------------------------------------------------------------------------------------------------------|:-----|
| --filter-severity          | Filter on specific notification severity. Can be 'normal' or 'urgent'. (Default: both severities shown).        | Mode |
| --filter-node              | Filter notifications by node ID. (Default: all notifications shown).                                            | Mode |
| --warning-notifications-*  | Set warning threshold for notifications count (Default: '') where '*' can be 'total', 'normal' or 'urgent'.     | Mode |
| --critical-notifications-* | Set critical threshold for notifications count (Default: '') where '*' can be 'total', 'normal' or 'urgent'.    | Mode |

</TabItem>
</Tabs>


All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins//centreon_graylog_restapi.pl \
	--plugin=apps::graylog::restapi::plugin \
	--mode=query \
    --help
```

### Troubleshooting

Please find the troubleshooting documentation for the API-based plugins in
this [chapter](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks).