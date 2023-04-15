---
id: applications-monitoring-alyvix-restapi
title: Alyvix Server
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Contenu du Pack

### Modèles

Le Plugin Pack Centreon **Alyvix Server RestAPI** apporte un modèle d'hôte :

* App-Monitoring-Alyvix-Restapi-custom-custom

Il apporte le modèle de service suivant :

| Alias            | Modèle de service                              | Description | Défaut | Découverte |
|:-----------------|:-----------------------------------------------|:------------|:-------|:-----------|
| Testcases-Global | App-Monitoring-Alyvix-Restapi-Testcases-Global | ContrÃ      | X      | X          |

> Les services par **Défaut** sont créés automatiquement lorsque le modèle d'hôte est appliqué.

> Si la case **Découverte** est cochée, cela signifie qu'une règle de découverte de service existe pour ce service.


### Règles de découverte

| Nom de la règle                             | Description |
|:--------------------------------------------|:------------|
| App-Monitoring-Alyvix-Restapi-Testcase-Name |             |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/services-discovery)
pour en savoir plus sur la découverte automatique de services et sa [planification](/docs/monitoring/discovery/services-discovery/#règles-de-découverte).

### Métriques & statuts collectés

<Tabs groupId="sync">
<TabItem value="Testcases-Global" label="Testcases-Global">

| Metric Name                       | Unité |
|:----------------------------------|:------|
| testcase.duration.milliseconds    | ms    |
| testcase-state                    | N/A   |
| testcase.freshness.seconds        | s     |
| transaction-state                 | N/A   |
| transaction.duration.milliseconds | ms    |

</TabItem>
</Tabs>

## Prérequis

*Specify prerequisites that are relevant. You may want to just provide a link
to the manufacturer official documentation BUT you should try to be as complete
as possible here as it will save time to everybody.*

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

Quel que soit le type de la licence (*online* ou *offline*), installez le Pack **Alyvix Server RestAPI**
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

### Hôte

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **App-Monitoring-Alyvix-Restapi-custom-custom**.
4. Une fois le modèle appliqué, les macros ci-dessous indiquées comme requises (**Obligatoire**) doivent être renseignées.

| Mandatory      | Macro             | Description                                                                       | Défaut  |
|:---------------|:------------------|:----------------------------------------------------------------------------------|:--------|
|                | ALYVIXAPIPASSWORD |                                                                                   |         |
|                | ALYVIXAPIPORT     | API port                                                                          | 80      |
|                | ALYVIXAPIPROTOCOL | Specify https if needed                                                           | http    |
|                | ALYVIXAPITIMEOUT  | Set HTTP timeout                                                                  |         |
|                | ALYVIXAPIURLPATH  | API url path                                                                      | /v0/    |
|                | ALYVIXAPIUSERNAME |                                                                                   |         |
|                | EXTRAOPTIONS      | Any extra option you may want to add to every command line (eg. a --verbose flag) |         |

### Service

| Mandatory      | Macro                       | Description                  | Défaut               |
|:---------------|:----------------------------|:-----------------------------|:---------------------|
|                | FILTERTESTCASE              | Filter on specific test case | .*                   |
|                | CRITICALTESTCASESTATE       |                              | %{state} eq "FAILED" |
|                | EXTRAOPTIONS                |                              | --verbose            |
|                | WARNINGTRANSACTIONSTATE     |                              |                      |
|                | CRITICALTRANSACTIONSTATE    |                              |                      |
|                | WARNINGTRANSACTIONDURATION  |                              |                      |
|                | CRITICALTRANSACTIONDURATION |                              |                      |
|                | WARNINGTESTCASEDURATION     |                              |                      |
|                | CRITICALTESTCASEDURATION    |                              |                      |
|                | WARNINGTESTCASESTATE        |                              |                      |
|                | WARNINGTESTCASEFRESHNESS    |                              |                      |
|                | CRITICALTESTCASEFRESHNESS   |                              |                      |

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`) :

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

La commande devrait retourner un message de sortie similaire à :

```bash
OK:      | 'testcase.duration.milliseconds'=2ms;;;0;;;;;  'testcase.freshness.seconds'=19s;;;0;;;;;  'transaction.duration.milliseconds'=84ms;;;0;;;;;  
```

### Modes disponibles

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_monitoring_alyvix_restapi.pl \
	--plugin=apps::monitoring::alyvix::restapi::plugin \
    --list-mode
```

Le plugin apporte les modes suivants :

| Mode           | Modèle de service associé                      |
|:---------------|:-----------------------------------------------|
| list-testcases | Used for service discovery                     |
| testcases      | App-Monitoring-Alyvix-Restapi-Testcases-Global |



### Options complémentaires

#### Options des modes

Les options spécifiques aux modes sont listées ci-dessus :

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


Pour un mode, la liste de toutes les options complémentaires et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_monitoring_alyvix_restapi.pl \
	--plugin=apps::monitoring::alyvix::restapi::plugin \
	--mode=testcases \
    --help
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks)
des plugins basés sur HTTP/API.