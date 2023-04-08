---
id: applications-monitoring-alyvix-restapi
title: Alyvix Server
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Pack Assets

### Templates

The Centreon Plugin Pack **Alyvix Server RestAPI** brings a host template:

* App-Monitoring-Alyvix-Restapi-custom-custom

It brings the following service template:

| Service Alias    | Service Template                               | Service Description                                                    | Default | Discovery |
|:-----------------|:-----------------------------------------------|:-----------------------------------------------------------------------|:--------|:----------|
| Testcases-Global | App-Monitoring-Alyvix-Restapi-Testcases-Global | Check the state and duration of "test cases" launched by Alyvix Server | X       | X         |


> **Default** services are automatically created when the host template is applied.
>
> If **Discovery** is checked, it means a service discovery rule exists for this service template.

### Discovery rules

| Rule Name                                   | Description |
|:--------------------------------------------|:------------|
| App-Monitoring-Alyvix-Restapi-Testcase-Name |             |

More information about discovering services automatically is available on the [dedicated page](/docs/monitoring/discovery/services-discovery)
and in the [following chapter](/docs/monitoring/discovery/services-discovery/#discovery-rules).

### Collected metrics & status

<Tabs groupId="sync">
<TabItem value="Testcases-Global" label="Testcases-Global">

| Metric Name                                       | Unit  |
|:--------------------------------------------------|:------|
| testcase.duration.milliseconds                    | ms    |
| testcase-state                                    |       |
| testcase.freshness.seconds                        | s     |
| cases~testcases#transaction-state                 |       |
| cases~testcases#transaction.duration.milliseconds | ms    |

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
dnf install centreon-pack-applications-monitoring-alyvix-restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-applications-monitoring-alyvix-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-monitoring-alyvix-restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-applications-monitoring-alyvix-restapi
```

</TabItem>
</Tabs>

Whatever the license type (*online* or *offline*), install the **Alyvix Server RestAPI** Pack through
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
dnf install centreon-plugin-Applications-Monitoring-Alyvix-Restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Applications-Monitoring-Alyvix-Restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Monitoring-Alyvix-Restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-applications-monitoring-alyvix-restapi
```

</TabItem>
</Tabs>

## Configuration

### Host

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill the **Name**, **Alias** & **IP Address/DNS** fields according to your ressource settings.
3. Apply the **App-Monitoring-Alyvix-Restapi-custom-custom** template to the host
4. Once the template is applied, fill in the corresponding macros. Some macros are mandatory.

| Mandatory      | Macro             | Description                                                                       | Default |
|:---------------|:------------------|:----------------------------------------------------------------------------------|:--------|
|                | ALYVIXAPIPASSWORD |                                                                                   |         |
|                | ALYVIXAPIPORT     | API port                                                                          | 80      |
|                | ALYVIXAPIPROTOCOL | Specify https if needed                                                           | http    |
|                | ALYVIXAPITIMEOUT  | Set HTTP timeout                                                                  |         |
|                | ALYVIXAPIURLPATH  | API url path                                                                      | /v0/    |
|                | ALYVIXAPIUSERNAME |                                                                                   |         |
|                | EXTRAOPTIONS      | Any extra option you may want to add to every command line (eg. a --verbose flag) |         |

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`) and test the plugin by
running the following command:

```bash
/usr/lib/centreon/plugins//centreon_monitoring_alyvix_restapi.pl \
	--plugin=apps::monitoring::alyvix::restapi::plugin \
	--mode=testcases \
	--hostname='10.0.0.1' \
	--port='' \
	--proto='' \
	--api-username='' \
	--api-password='' \
	--url-path='' \
	--timeout=''  \
	--filter-testcase='' \
	--warning-transaction-state='' \
	--critical-transaction-state='' \
	--warning-transaction-duration='' \
	--critical-transaction-duration='' \
	--warning-testcase-duration='' \
	--critical-testcase-duration='' \
	--warning-testcase-state='' \
	--critical-testcase-state='' \
	--warning-testcase-freshness='' \
	--critical-testcase-freshness='' \
	
```

The expected command output is shown below:

```bash
OK:      | 'testcase.duration.milliseconds'=7ms;;;0; 'testcase.freshness.seconds'=90s;;;0; 'transaction.duration.milliseconds'=67ms;;;0; 
```

### Available modes

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins//centreon_monitoring_alyvix_restapi.pl \
	--plugin=apps::monitoring::alyvix::restapi::plugin \
    --list-mode
```

The plugin brings the following modes:

| Mode           | Template                                       |
|:---------------|:-----------------------------------------------|
| list-testcases | Used for service discovery                     |
| testcases      | App-Monitoring-Alyvix-Restapi-Testcases-Global |



### Available options

#### Modes options

All  modes specific options are listed here:

<Tabs groupId="sync">
<TabItem value="Testcases-Global" label="Testcases-Global">

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
| --source-encoding                          | Set encoding of monitoring sources (In some case. Default: 'UTF-8').      Alyvix Server Rest API.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Output       |
| --hostname                                 | Alyvix Server hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Api          |
| --url-path                                 | API url path (Default: '/v0/')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Api          |
| --port                                     | API port (Default: 80)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Api          |
| --proto                                    | Specify https if needed (Default: 'http')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Api          |
| --credentials                              | Specify this option if you access the API with authentication                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Api          |
| --username                                 | Specify username for authentication (Mandatory if --credentials is specified)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Api          |
| --password                                 | Specify password for authentication (Mandatory if --credentials is specified)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Api          |
| --basic                                    | Specify this option if you access the API over basicauthentication and don't want a '401 UNAUTHORIZED' error to be logged on your webserver.  Specify this option if you access the API over hidden basic authentication or you'll get a '404 NOT FOUND' error.  (Use with --credentials)                                                                                                                                                                                                                                                                                  | Api          |
| --timeout                                  | Set HTTP timeout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Api          |
| --http-peer-addr                           | Set the address you want to connect (Useful if hostname is only a vhost. no ip resolve)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Http global  |
| --proxyurl                                 | Proxy URL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Http global  |
| --proxypac                                 | Proxy pac file (can be an url or local file)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Http global  |
| --insecure                                 | Insecure SSL connections.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Http global  |
| --http-backend                             | Set the backend used (Default: 'lwp') For curl: --http-backend=curl                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Http global  |
| --ssl-opt                                  | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Backend lwp  |
| --ssl                                      | Set SSL version (=TLSv1).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Backend lwp  |
| --curl-opt                                 | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                                                                                                                                                                                                                                                                                                                                                           | Backend curl |
| --hostname                                 | ='10.0.0.1'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Mode         |
| --filter-testcase                          | Filter on specific test case.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Mode         |
| --warning-*-state                          | Set warning status (Default: '') where '*' can be 'testcase' or 'transaction'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Mode         |
| --critical-*-state                         | Set critical status (Default: '%{state} eq "FAILED"') where '*' can be 'testcase' or 'transaction'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Mode         |
| --warning-*-duration                       | Set warning threshold for test cases or transactions duration (Default: '') where '*' can be 'testcase' or 'transaction'.                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Mode         |
| --critical-*-duration                      | Set critical threshold for test cases or transactions duration (Default: '') where '*' can be 'testcase' or 'transaction'.                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Mode         |

</TabItem>
</Tabs>


All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins//centreon_monitoring_alyvix_restapi.pl \
	--plugin=apps::monitoring::alyvix::restapi::plugin \
	--mode=testcases \
    --help
```

### Troubleshooting

Please find the troubleshooting documentation for the API-based plugins in
this [chapter](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks).