---
id: applications-antivirus-kaspersky-snmp
title: Kaspersky
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Contenu du Pack

### Modèles

Le Plugin Pack Centreon **Kaspersky** apporte un modèle d'hôte :

* App-Antivirus-Kaspersky-SNMP-custom-custom

Il apporte les modèles de service suivants :

| Alias           | Modèle de service                            | Description                                                                                   | Défaut |
|:----------------|:---------------------------------------------|:----------------------------------------------------------------------------------------------|:-------|
| Deployment      | App-Antivirus-Kaspersky-Deployment-SNMP      | Contrôle le statut du déploiement                                                             | X      |
| Events          | App-Antivirus-Kaspersky-Events-SNMP          | Contrôle le statut des évènements                                                             | X      |
| Full-Scan       | App-Antivirus-Kaspersky-Full-Scan-SNMP       | Contrôle le statut des scans                                                                  | X      |
| Logical-Network | App-Antivirus-Kaspersky-Logical-Network-SNMP | Contrôle le statut de la découverte réseau                                                    | X      |
| Protection      | App-Antivirus-Kaspersky-Protection-SNMP      | Contrôle le statut de la protection                                                           | X      |
| Updates         | App-Antivirus-Kaspersky-Updates-SNMP         | Contrôle le temps depuis la dernière mise à jour du serveur et le nombre de client non à jour | X      |

> Les services par **Défaut** sont créés automatiquement lorsque le modèle d'hôte est appliqué.


### Métriques & statuts collectés

<Tabs groupId="sync">
<TabItem value="Deployment" label="Deployment">

| Metric Name                          | Unité |
|:-------------------------------------|:------|
| status                               | N/A   |
| hosts.antivirus.installed.count      | count |
| hosts.antivirus.install.failed.count | count |
| hosts.expiring.licence.count         | count |
| hosts.expired.licence.count          | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
<TabItem value="Events" label="Events">

| Metric Name           | Unité |
|:----------------------|:------|
| status                | N/A   |
| events.critical.count | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
<TabItem value="Full-Scan" label="Full-Scan">

| Metric Name           | Unité |
|:----------------------|:------|
| status                | N/A   |
| hosts.unscanned.count | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
<TabItem value="Logical-Network" label="Logical-Network">

| Metric Name              | Unité |
|:-------------------------|:------|
| status                   | N/A   |
| hosts.new.count          | count |
| groups.total.count       | count |
| hosts.notconnected.count | count |
| hosts.uncontrolled.count | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
<TabItem value="Protection" label="Protection">

| Metric Name                                        | Unité |
|:---------------------------------------------------|:------|
| status                                             | N/A   |
| protection.hosts.antivirus.notrunning.count        | count |
| protection.hosts.realtime.notrunning.count         | count |
| protection.hosts.realtime.unacceptable.level.count | count |
| protection.hosts.uncured.objects.count             | count |
| protection.hosts.toomanythreats.count              | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
<TabItem value="Updates" label="Updates">

| Metric Name                     | Unité |
|:--------------------------------|:------|
| status                          | N/A   |
| update.server.freshness.seconds | s     |
| update.hosts.outdated.count     | count |

> L'option **--use-new-perfdata** est nécessaire pour avoir le nouevau format de métrique.

</TabItem>
</Tabs>

## Prérequis

### Configuration SNMP

Afin de superviser votre ressource en SNMP,  il est nécessaire de configurer l'agent sur le serveur comme indiqué sur la documentation officielle :
* LINK

### Flux réseau

La communication doit être possible sur le port UDP 161 depuis le collecteur
Centreon vers le serveur supervisé.

## Installation

### Pack de supervision

Si la plateforme est configurée avec une licence *online*, l'installation d'un paquet
n'est pas requise pour voir apparaître le pack dans le menu **Configuration > Plugin Packs > Gestionnaire**.

Au contraire, si la plateforme utilise une licence *offline*, installez le paquet
sur le **serveur central** via la commande correspondant au gestionnaire de paquet
associé à sa distribution :

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

Quel que soit le type de la licence (*online* ou *offline*), installez le Pack **Kaspersky**
depuis l'interface web et le menu **Configuration > Plugin Packs > Gestionnaire**.

### Plugin

À partir de Centreon 22.04, il est possible de demander le déploiement automatique
du plugin lors de l'utilisation d'un pack. Si cette fonctionnalité est activée, et
que vous ne souhaitez pas découvrir des éléments pour la première fois, alors cette
étape n'est pas requise.

> Plus d'informations dans la section [Installer le plugin](/docs/monitoring/pluginpacks/#installer-le-plugin).

Utilisez les commandes ci-dessous en fonction du gestionnaire de paquets de votre système d'exploitation :

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

### Hôte

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **App-Antivirus-Kaspersky-SNMP-custom-custom**.
4. Une fois le modèle appliqué, les macros ci-dessous indiquées comme requises (**Obligatoire**) doivent être renseignées.

| Mandatory      | Macro            | Description                                                                       | Défaut  |
|:---------------|:-----------------|:----------------------------------------------------------------------------------|:--------|
|                | SNMPEXTRAOPTIONS | Any extra option you may want to add to every command line (eg. a --verbose flag) |         |

### Service

<Tabs groupId="sync">
<TabItem value="Deployment" label="Deployment">

| Mandatory      | Macro            | Description                                                                                                         | Défaut                   |
|:---------------|:-----------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS    | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS   | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGPROGRESS  |                                                                                                                     | 100:                     |
|                | CRITICALPROGRESS |                                                                                                                     | 95:                      |
|                | WARNINGFAILED    |                                                                                                                     | 0                        |
|                | WARNINGEXPIRING  |                                                                                                                     | 0                        |
|                | WARNINGEXPIRED   |                                                                                                                     | 0                        |
|                | CRITICALFAILED   |                                                                                                                     |                          |
|                | CRITICEXPIRING   |                                                                                                                     |                          |
|                | CRITICALEXPIRED  |                                                                                                                     |                          |

</TabItem>
<TabItem value="Events" label="Events">

| Mandatory      | Macro          | Description                                                                                                         | Défaut                   |
|:---------------|:---------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS  | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGEVENTS  |                                                                                                                     | 0                        |
|                | CRITICALEVENTS |                                                                                                                     |                          |

</TabItem>
<TabItem value="Full-Scan" label="Full-Scan">

| Mandatory      | Macro              | Description                                                                                                         | Défaut                   |
|:---------------|:-------------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS      | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS     | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGNOTSCANNED  |                                                                                                                     | 0                        |
|                | CRITICALNOTSCANNED |                                                                                                                     |                          |

</TabItem>
<TabItem value="Logical-Network" label="Logical-Network">

| Mandatory      | Macro                        | Description                                                                                                         | Défaut                   |
|:---------------|:-----------------------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS                | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS               | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGNOTCONNECTEDLONGTIME  |                                                                                                                     | 0                        |
|                | WARNINGNOTCONTROLLED         |                                                                                                                     | 0                        |
|                | WARNINGNEWHOSTS              |                                                                                                                     |                          |
|                | CRITICALNEWHOSTS             |                                                                                                                     |                          |
|                | WARNINGGROUPS                |                                                                                                                     |                          |
|                | CRITICALGROUPS               |                                                                                                                     |                          |
|                | CRITICALNOTCONNECTEDLONGTIME |                                                                                                                     |                          |
|                | CRITICALNOTCONTROLLED        |                                                                                                                     |                          |

</TabItem>
<TabItem value="Protection" label="Protection">

| Mandatory      | Macro                      | Description                                                                                                         | Défaut                   |
|:---------------|:---------------------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS              | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS             | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGNOANTIVIRUS         |                                                                                                                     | 0                        |
|                | WARNINGNOREALTIME          |                                                                                                                     | 0                        |
|                | WARNINGNOTACCEPTABLELEVEL  |                                                                                                                     | 0                        |
|                | WARNINGNOTCUREDOBJECTS     |                                                                                                                     | 0                        |
|                | WARNINGTOOMANYTHREATS      |                                                                                                                     | 0                        |
|                | CRITICALNOANTIVIRUS        |                                                                                                                     |                          |
|                | CRITICALNOREALTIME         |                                                                                                                     |                          |
|                | CRITICALNOTACCEPTABLELEVEL |                                                                                                                     |                          |
|                | CRITICALNOTCUREDOBJECTS    |                                                                                                                     |                          |
|                | CRITICALTOOMANYTHREATS     |                                                                                                                     |                          |

</TabItem>
<TabItem value="Updates" label="Updates">

| Mandatory      | Macro                    | Description                                                                                                         | Défaut                   |
|:---------------|:-------------------------|:--------------------------------------------------------------------------------------------------------------------|:-------------------------|
|                | WARNINGSTATUS            | Set warning threshold for status. (Default: '%{status} =~ /Warning/i'). Can use special variables like: %{status}   | %{status} =~ /Warning/i  |
|                | CRITICALSTATUS           | Set critical threshold for status. (Default: '%{status} =~ /Critical/i'). Can use special variables like: %{status} | %{status} =~ /Critical/i |
|                | WARNINGLASTSERVERUPDATE  |                                                                                                                     | 120                      |
|                | CRITICALLASTSERVERUPDATE |                                                                                                                     | 240                      |
|                | WARNINGNOTUPDATED        |                                                                                                                     | 0                        |
|                | CRITICALNOTUPDATED       |                                                                                                                     |                          |

</TabItem>
</Tabs>

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`) :

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
	--mode=deployment \
	--hostname=10.0.0.1 \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community'  \
	--warning-status='' \
	--critical-status='' \
	--warning-progress='' \
	--critical-progress='' \
	--warning-failed='' \
	--critical-failed='' \
	--warning-expiring='' \
	--critical-expiring='' \
	--warning-expired='' \
	--critical-expired='' \
	
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK:      | 'hosts.antivirus.installed.count'=50;;;0;;;;;  'hosts.antivirus.install.failed.count'=60;;;0 ;;;;;  'hosts.expiring.licence.count'=81;;;0;;;;;  'hosts.expired.licence.count'=34;;;0;;;;;  
```

### Modes disponibles

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
    --list-mode
```

Le plugin apporte les modes suivants :

| Mode            | Modèle de service associé                    |
|:----------------|:---------------------------------------------|
| deployment      | App-Antivirus-Kaspersky-Deployment-SNMP      |
| events          | App-Antivirus-Kaspersky-Events-SNMP          |
| full-scan       | App-Antivirus-Kaspersky-Full-Scan-SNMP       |
| logical-network | App-Antivirus-Kaspersky-Logical-Network-SNMP |
| protection      | App-Antivirus-Kaspersky-Protection-SNMP      |
| updates         | App-Antivirus-Kaspersky-Updates-SNMP         |



### Options complémentaires

#### Options globales

Les options globales aux modes sont listées ci-dessus :

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
| --hostname                                 | Hostname to query (required).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | SNMP   |
| --snmp-community                           | Read community (defaults to public).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | SNMP   |
| --snmp-version                             | Version: 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | SNMP   |
| --snmp-port                                | Port (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | SNMP   |
| --snmp-timeout                             | Timeout in secondes (default: 1) before retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | SNMP   |
| --snmp-retries                             | Set the number of retries (default: 5) before failure.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | SNMP   |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | SNMP   |
| --subsetleef                               | How many oid values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                   | SNMP   |
| --snmp-autoreduce                          | Auto reduce SNMP request size in case of SNMP errors (By default, the divisor is 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | SNMP   |
| --snmp-force-getnext                       | Use snmp getnext function (even in snmp v2c and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | SNMP   |
| --snmp-username                            | Security name (only for SNMP v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | SNMP   |
| --authpassphrase                           | Authentication protocol pass phrase.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | SNMP   |
| --authprotocol                             | Authentication protocol: MD5\|SHA. Since net-snmp 5.9.1: SHA224\|SHA256\|SHA384\|SHA512.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | SNMP   |
| --privpassphrase                           | Privacy protocol pass phrase                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | SNMP   |
| --privprotocol                             | Privacy protocol: DES\|AES. Since net-snmp 5.9.1: AES192\|AES192C\|AES256\|AES256C.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | SNMP   |
| --contextname                              | Context name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | SNMP   |
| --contextengineid                          | Context engine ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | SNMP   |
| --securityengineid                         | Security engine ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | SNMP   |
| --snmp-errors-exit                         | Exit code for SNMP Errors (default: unknown)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | SNMP   |
| --snmp-tls-transport                       | TLS Transport communication used (can be: 'dtlsudp', 'tlstcp').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | SNMP   |
| --snmp-tls-our-identity                    | Our X.509 identity to use, which should either be a fingerprint or the filename that holds the certificate.                                                                                                                                                                                                                                                                                                                                                                                                                                                                | SNMP   |
| --snmp-tls-their-identity                  | The remote server's identity to connect to, specified as either a fingerprint or a file name. Either this must be specified, or the hostname below along with a trust anchor.                                                                                                                                                                                                                                                                                                                                                                                              | SNMP   |
| --snmp-tls-their-hostname                  | The remote server's hostname that is expected. If their certificate was signed by a CA then their hostname presented in the certificate must match this value or the connection fails to be established (to avoid man-in-the-middle attacks).                                                                                                                                                                                                                                                                                                                              | SNMP   |
| --snmp-tls-trust-cert                      | A trusted certificate to use as trust anchor (like a CA certificate) for verifying a remote server's certificate. If a CA certificate is used to validate a certificate then the TheirHostname parameter must also be specified to ensure their presented hostname in the certificate matches.                                                                                                                                                                                                                                                                             | SNMP   |


#### Options des modes

Les options spécifiques aux modes sont listées ci-dessus :

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


Pour un mode, la liste de toutes les options complémentaires et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_kaspersky_snmp.pl \
	--plugin=apps::antivirus::kaspersky::snmp::plugin \
	--mode=deployment \
    --help
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md)
pour le diagnostic des erreurs communes des plugins Centreon.