---
title: Tough Day
seo-title: Jour difficile
description: Le test Tough Day simule la charge quotidienne d’environ 1 000 auteurs dans le pire des scénarios, toutes les opérations se déroulant simultanément.
seo-description: Le test Tough Day simule la charge quotidienne d’environ 1 000 auteurs dans le pire des scénarios, toutes les opérations se déroulant simultanément.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
translation-type: tm+mt
source-git-commit: 3727b561a2ee9778d75f18530caf16c6c3ef846a
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 53%

---

# Jour difficile{#tough-day}

## Qu’est-ce que Tough Day 2 ?{#what-is-tough-day}

« Tough Day 2 » est une application qui vous permet de tester les limites de votre instance AEM. Prête à l’emploi, elle peut être exécutée avec la suite de tests par défaut ou configurée pour répondre à vos impératifs de test. [Cet enregistrement](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) est une présentation de l’application.

## Comment exécuter jusqu&#39;au 2e jour {#how-to-run-tough-day}

Téléchargez la dernière version de Tough Day 2 à partir du [référentiel Adobe](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/). Après avoir téléchargé l’application, vous pouvez l’exécuter en dehors de la zone en fournissant le paramètre `host`. Dans l’exemple suivant, l’instance AEM s’exécute localement afin que la valeur `localhost` soit utilisée :

```xml
java -jar toughday2.jar --host=localhost
```

La suite par défaut qui s’exécute après l’ajout des paramètres s’appelle `toughday`. Elle contient les cas d’utilisation suivants :

* Créer des pages et des copies en direct pour eux (y compris les déploiements)
* Obtenir la page d’accueil
* Exécuter des requêtes dans le générateur de requêtes
* Créer des hiérarchies de ressources
* Suppression des ressources

La suite contient 15 % d’actions d’écriture et 85 % d’actions de lecture.

Pour exécuter les tests de la suite, Tough Day 2 installe son package de contenu par défaut. Cela peut être évité en définissant le paramètre `installsamplecontent`sur `false`, mais n&#39;oubliez pas que vous devez également modifier les chemins par défaut pour les tests que vous prévoyez d&#39;exécuter. Si le fichier jar est exécuté sans paramètres, Tough Day 2 affiche les [informations d&#39;aide](/help/sites-developing/tough-day.md#getting-help).

En règle générale, vous pouvez utiliser l’application en suivant ce modèle :

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 n’a pas d’étape de nettoyage. Par conséquent, il est recommandé d’exécuter Tough Day 2 sur une instance de transfert clonée et non sur l’instance de production principale. L’instance de transfert doit être supprimée après les tests.


### Obtenir de l’aide {#getting-help}

Tough Day 2 offre un large éventail d’options d’aide accessibles depuis la ligne de commande. Par exemple :

```xml
java -jar toughday2.jar --help_full
```

Le tableau ci-dessous décrit des paramètres d’aide pertinents.

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
   <td><strong>Exemple</strong></td>
  </tr>
  <tr>
   <td>--help</td>
   <td>Imprime des informations globales, par exemple : les actions disponibles, les suites prédéfinies, les modes d'exécution et les paramètres globaux.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Imprime tous les éditeurs disponibles.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>Imprime les classes de test et leur description.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Imprime tous les éléments ci-dessus, ainsi que les tests, les éditeurs et les composants de la suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>Liste des informations sur le mode d’exécution ou de publication spécifié.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervalles</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;NomSuite&gt;</td>
   <td>Liste tous les tests d’une suite donnée et leurs propriétés configurables respectives.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Balise&gt;</td>
   <td><br /> Liste tous les éléments qui ont la balise spécifiée.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Liste toutes les propriétés configurables pour le test ou l’éditeur donné.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPubliher</p> </td>
  </tr>
 </tbody>
</table>

### Paramètres globaux {#global-parameters}

Tough Day 2 propose des paramètres globaux qui définissent ou modifient l’environnement pour les tests. Ils incluent notamment l’hôte ciblé, le numéro de port, le protocole utilisé, l’utilisateur et le mot de passe pour l’instance et bien d’autres. Par exemple :

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Voici la liste des paramètres pertinents :

| **Paramètre** | **Description** | **Valeur par défaut** | **Valeurs possibles** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installe ou ignore le package de contenu par défaut, Tough Day 2. | true | true ou false |
| `--protocol=<Val>` | Protocole utilisé pour l’hôte. | http | http ou https |
| `--host=<Val>` | Nom d’hôte ou adresse IP qui sera ciblé. |  |  |
| `--port=<Val>` | Port de l’hôte. | 4502 |  |
| `--user=<Val>` | Nom d’utilisateur de l’instance. | admin |  |
| `--password=<Val>` | Mot de passe pour l’utilisateur donné. | admin |  |
| `--duration=<Val>` | Durée des tests. Peut être exprimé en (**s**)secondes, (**m**)minutes (**h**)nours et (**d**) jours. | 1d |  |
| `--timeout=<Val>` | Durée pendant laquelle un test s&#39;exécute avant d&#39;être interrompu et signalé comme échec. Exprimé en secondes. | 180 |  |
| `--suite=<Val>` | La valeur peut être une ou une liste (séparée par des virgules) de suites de tests prédéfinies. | jour difficile |  |
| `--configfile=<Val>` | Le fichier de configuration de l&#39;image cible. |  |  |
| `--contextpath=<Val>` | Chemin d’accès contextuel de l’instance. |  |  |
| `--loglevel=<Val>` | Niveau de journal du moteur de journée difficile 2. | INFO | TOUT, DÉBOGUER, INFORMATIONS, AVERTISSEMENT, ERREUR, FATAL, OFF |
| `--dryrun=<Val>` | Si la valeur est true, imprime la configuration résultante et n’exécute aucun test. | false | true ou false |

## Personnalisation {#customizing}

La personnalisation peut être réalisée de deux manières : avec les paramètres de ligne de commande ou les fichiers de configuration yaml. **Les fichiers de configuration sont généralement utilisés pour les grandes suites personnalisées. Ils remplacent les paramètres par défaut de Tough Day 2. Les paramètres de ligne de commande remplacent les fichiers de configuration et les paramètres par défaut.**

La seule façon d’enregistrer une configuration de test consiste à la copier au format yaml. Pour plus d&#39;informations, reportez-vous à cette configuration [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) et aux exemples de configuration de l&#39;année dans les sections ci-dessous.

### Ajout d’un test {#adding-a-new-test}

Si vous ne voulez pas utiliser la suite `toughday` par défaut, vous pouvez ajouter un test de votre choix en utilisant le paramètre `add`. Les exemples ci-dessous montrent comment ajouter le test `CreateAssetTreeTest` en utilisant des paramètres de ligne de commande ou un fichier de configuration yaml.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Ajout de plusieurs instances du même test  {#adding-multiple-instances-of-the-same-test}

Vous pouvez également ajouter et exécuter plusieurs instances du même test, mais chaque instance doit avoir un nom unique. Les exemples ci-dessous montrent comment ajouter deux instances du même test en utilisant des paramètres de ligne de commande ou un fichier de configuration yaml.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### Modification des propriétés de test {#changing-the-test-properties}

Si vous devez modifier une ou plusieurs propriétés de test, vous pouvez ajouter cette propriété à la ligne de commande ou au fichier de configuration yaml. Pour afficher toutes les propriétés de test disponibles, ajoutez le paramètre `--help <TestClass/PublisherClass>` à la ligne de commande, par exemple :

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Gardez à l’esprit que les fichiers de configuration yaml écraseront les paramètres par défaut de Tough Day 2 et que les paramètres de ligne de commande remplaceront les fichiers de configuration et les valeurs par défaut.

Les exemples ci-dessous montrent comment modifier la propriété `template` pour le test `CreatePageTreeTest` en utilisant soit des paramètres de ligne de commande, soit un fichier de configuration yaml.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Utilisation de suites de tests prédéfinies  {#working-with-predefined-test-suites}

Les exemples ci-dessous montrent comment ajouter un test à une suite prédéfinie et comment reconfigurer et exclure un test existant d’une suite prédéfinie.

Vous pouvez ajouter un nouveau test à une suite prédéfinie en utilisant le paramètre `add` et en spécifiant la suite prédéfinie ciblée.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Les tests existants dans une suite donnée peuvent également être reconfigurés à l’aide du paramètre *a0/>*. `config` Veuillez noter que vous devez également indiquer le nom de la suite et le nom réel du test (et non le nom de la classe de test). Le nom du test est disponible dans la propriété `name` de la classe de test. Pour savoir comment retrouver les propriétés de test, lisez la section [Modification des propriétés de test](/help/sites-developing/tough-day.md#changing-the-test-properties).

Dans l’exemple ci-dessous, le titre de ressource par défaut de `CreatePageTreeTest` (nommé `UploadAsset`) est remplacé par &quot;NewAsset&quot;.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

En outre, vous pouvez également supprimer les tests des suites prédéfinies ou des éditeurs de la configuration par défaut à l’aide du paramètre `exclude`. Veuillez noter que vous devez également indiquer le nom de la suite et le nom réel du test (et non le nom du test C `lass`). Vous pouvez trouver le nom du test dans la propriété `name` de la classe de test. Dans l’exemple ci-dessous, le test `CreatePageTreeTest` (nommé `UploadAsset`) est supprimé de la suite de jours difficiles.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modes d’exécution  {#run-modes}

Le jour difficile 2 peut s’exécuter dans l’un des modes suivants : **charge normale** et **charge constante**.

Le mode d&#39;exécution **normal** comporte deux paramètres :

* `concurrency` - concurrence représente le nombre de threads que Tough Day 2 va créer pour l&#39;exécution du test. Sur ces threads, les tests sont exécutés jusqu’à ce que la durée soit écoulée ou qu’il n’y ait plus de tests à exécuter.

* `waittime` : temps d’attente entre deux exécutions de test consécutives sur le même thread. La valeur doit être exprimée en millisecondes.

L’exemple ci-dessous montre comment ajouter les paramètres au moyen de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

ou en utilisant un fichier de configuration yaml :

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

Le mode d&#39;exécution **charge constante** diffère du mode d&#39;exécution normal en générant un nombre constant d&#39;exécutions de tests démarrées, plutôt qu&#39;un nombre constant de threads. Vous pouvez définir le chargement à l’aide du paramètre du mode d’exécution portant le même nom.

### Sélection de test {#test-selection}

Le processus de sélection des tests est le même pour les deux modes d’exécution et se présente comme suit : tous les tests ont une propriété `weight` qui détermine la probabilité d’exécution dans un thread. Prenons l’exemple de deux tests, l’un avec une pondération de 5 et l’autre de 10. Dans ce cas, ce dernier a deux fois plus de chance d’être exécuté que le premier.

En outre, les tests peuvent avoir une propriété `count`, qui limite le nombre d’exécutions à un nombre donné. Une fois ce nombre atteint, aucune autre exécution du test n’aura lieu. Toutes les instances de test en cours d’exécution se terminent selon leur configuration. L’exemple suivant montre comment ajouter ces paramètres à l’aide de la ligne de commande ou d’un fichier de configuration yaml.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

ou

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>En raison d’exécutions parallèles, le nombre réel d’exécutions de test ne correspond pas exactement à la quantité configurée dans le paramètre `count`. Attendez-vous à un écart proportionnel au nombre de threads en cours d&#39;exécution (contrôlé par `concurrency parameter`).

### Exécution d’essai {#dry-run}

Une analyse à sec étudie toutes les entrées données (paramètres de ligne de commande ou fichiers de configuration), les fusionne avec les valeurs par défaut, puis affiche les résultats. Elle n’exécute aucun des tests.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Sortie {#output}

Tough Day 2 génère à la fois des métriques de test et des journaux. Pour plus de détails, lisez les sections suivantes.

### Métriques de test  {#test-metrics}

Tough Day 2 fait actuellement état de 9 métriques de test que vous pouvez évaluer. Les mesures avec le symbole ***** ne sont reportées qu’après des exécutions réussies :

| **Name** (Nom) | **Description** |
|---|---|
| Timestamp | Horodatage de la dernière exécution de test terminée. |
| Transmis | Nombre d&#39;exécutions réussies. |
| Échec | Nombre d&#39;exécutions ayant échoué. |
| Min* | Durée la plus faible d’exécution du test. |
| Max* | Durée d’exécution du test la plus élevée. |
| Médiane* | Durée médiane calculée de toutes les exécutions de test. |
| Moyenne* | Durée moyenne calculée de toutes les exécutions de test. |
| StdDev* | Écart type. |
| 90p* | 90 centile. |
| 99p* | 99 pour cent. |
| 99.9p* | 99,9 centile. |
| Débit réel* | Nombre d’exécutions divisé par le temps d’exécution écoulé. |

Ces mesures sont écrites à l’aide d’éditeurs qui peuvent être ajoutées avec le paramètre `add` (de la même manière que l’ajout de tests). Actuellement, il existe deux options :

* **CSVPubliher**  : la sortie est un fichier CSV.
* **ConsolePublisher**  : la sortie s&#39;affiche dans la console.

Par défaut, les deux éditeurs sont activés.

En outre, il existe deux modes dans lesquels les mesures sont rapportées :

* Le mode de publication **simple** signale les résultats du début de l’exécution jusqu’au point de publication.
* Le mode de publication **intervalles** signale les résultats dans une période donnée. Vous pouvez définir la période avec le paramètre du mode de publication **interval**.

L&#39;exemple suivant montre comment configurer le paramètre `intervals` en ligne de commande ou à l&#39;aide d&#39;un fichier de configuration yaml.

En utilisant les paramètres de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

En utilisant un fichier de configuration yaml :

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Journalisation {#logging}

Tough Day 2 crée un dossier de journaux dans le même répertoire que celui où vous avez exécuté Tough Day 2. Ce dossier contient deux types de journaux :

* **toughday.log** : contient les messages relatifs à l’état de l’application, aux informations de débogage et aux messages d’ordre général.
* **toughday_&lt;testname>.log** : messages liés au test spécifié.

Les journaux ne sont pas remplacés, les exécutions subséquentes ajoutent des messages aux journaux existants. Les journaux ont plusieurs niveaux, pour plus d&#39;informations voir le ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Exemple d’utilisation  {#example-usage}

#### Problèmes connus {#known-issues}

[Obtenir le fichier](assets/toughday-6_1.jar)
