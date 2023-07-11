---
title: Tough Day
description: Le test Tough Day simule la charge quotidienne d’environ 1 000 auteurs dans le pire des cas, avec toutes les opérations en même temps.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 63%

---

# Tough Day{#tough-day}

## Qu’est-ce que Tough Day 2 ? {#what-is-tough-day}

« Tough Day 2 » est une application qui vous permet de tester les limites de votre instance AEM. Prête à l’emploi, elle peut être exécutée avec la suite de tests par défaut ou configurée pour répondre à vos impératifs de test. Vous pouvez regarder [cet enregistrement](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) pour une présentation de l’application.

>[!CAUTION]
>
>Tough Day 2 nécessite Java™ 8.

## Procédure d’exécution de Tough Day 2 {#how-to-run-tough-day}

Téléchargez la dernière version de Tough Day 2 à partir du [référentiel Adobe](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). Après avoir téléchargé l’application, vous pouvez l’extraire en fournissant le paramètre `host`. Dans l’exemple suivant, l’instance AEM s’exécute localement, de sorte que la valeur `localhost` est utilisée :

```xml
java -jar toughday2.jar --host=localhost
```

La suite par défaut qui s’exécute après l’ajout des paramètres s’appelle `toughday`. Il contient les cas d’utilisation suivants :

* Créer des pages et des Live Copies pour elles (y compris les déploiements)
* Obtenir la page d’accueil
* Exécution de requêtes dans querybuilder
* Création de hiérarchies de ressources
* Suppression des ressources

La suite contient 15 % d’actions d’écriture et 85 % d’actions de lecture.

Pour exécuter les tests de la suite, Tough Day 2 installe son package de contenu par défaut. Cela peut être évité en définissant le paramètre `installsamplecontent` sur `false`, mais souvenez-vous que vous devez également modifier les chemins par défaut pour les tests que vous avez l’intention d’exécuter. Si le jar est exécuté sans paramètres, Tough Day 2 affiche les [informations d’aide](/help/sites-developing/tough-day.md#getting-help).

En règle générale, vous pouvez utiliser l’application en suivant ce modèle :

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
Tough Day 2 n’a pas d’étape de nettoyage. Par conséquent, il est recommandé d’exécuter Tough Day 2 sur une instance de transfert clonée et non sur l’instance de production principale. L’instance d’évaluation doit être supprimée après les tests.
>

### Obtention d’aide {#getting-help}

Tough Day 2 offre un large éventail d’options d’aide accessibles depuis la ligne de commande. Par exemple :

```xml
java -jar toughday2.jar --help_full
```

Dans le tableau ci-dessous, vous trouverez les paramètres d’aide pertinents.

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
   <td><strong>Exemple</strong></td>
  </tr>
  <tr>
   <td>--help</td>
   <td>Imprime des informations globales, par exemple les actions disponibles, les suites prédéfinies, les modes d’exécution et les paramètres globaux.</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_publish</td>
   <td>Imprime tous les éditeurs disponibles.</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_tests</td>
   <td>Imprime les classes de test et leur description.</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_full</td>
   <td>Imprime tous les éléments ci-dessus, ainsi que les tests, les éditeurs et les composants de la suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> --help --runmode/publishmode type=&lt;Mode&gt;</td>
   <td>Répertorie les informations sur le mode d’exécution ou de publication spécifié.</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>--help --suite=&lt;SuiteName&gt;</td>
   <td>Répertorie tous les tests d’une suite donnée et leurs propriétés configurables respectives.</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> --help --tag=&lt;Tag&gt;</td>
   <td><br /> Répertorie tous les éléments qui possèdent la balise spécifiée.</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>--help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Répertorie toutes les propriétés configurables pour le test ou l’éditeur donné.</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Paramètres globaux {#global-parameters}

Tough Day 2 propose des paramètres globaux qui définissent ou modifient l’environnement pour les tests. Ils incluent notamment l’hôte ciblé, le numéro de port, le protocole utilisé, l’utilisateur et le mot de passe pour l’instance et bien d’autres. Par exemple :

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Vous trouverez les paramètres appropriés dans la liste ci-dessous :

| **Paramètre** | **Description** | **Valeur par défaut** | **Valeurs possibles** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installe ou ignore le package de contenu Tough Day 2 par défaut. | true | true ou false |
| `--protocol=<Val>` | Protocole utilisé pour l’hôte. | http | http ou https |
| `--host=<Val>` | Nom d’hôte ou adresse IP qui sera ciblé. |  |  |
| `--port=<Val>` | Port de l’hôte. | 4502 |  |
| `--user=<Val>` | Nom d’utilisateur de l’instance. | admin |  |
| `--password=<Val>` | Mot de passe pour ce même utilisateur. | admin |  |
| `--duration=<Val>` | Durée des tests. Peut être exprimée en (**s**)econdes, (**m**)inutes, (**h**)eures et (**j**)ours. | 1d |  |
| `--timeout=<Val>` | Durée pendant laquelle un test s’exécute avant d’être interrompu et marqué comme ayant échoué. Exprimée en secondes. | 180 |  |
| `--suite=<Val>` | La valeur peut être une ou une liste (séparée par des virgules) de suites de tests prédéfinies. | toughday |  |
| `--configfile=<Val>` | Le fichier de configuration yaml ciblé. |  |  |
| `--contextpath=<Val>` | Chemin d’accès au contexte de l’instance. |  |  |
| `--loglevel=<Val>` | Niveau de journal du moteur Tough Day 2. | INFO | ALL, DEBUG, INFO, WARN, ERROR, FATAL, OFF |
| `--dryrun=<Val>` | Si la valeur est true, imprime la configuration obtenue et n’exécute aucun test. | false | true ou false |

## Personnalisation {#customizing}

La personnalisation peut être réalisée de deux manières : paramètres de ligne de commande ou fichiers de configuration yaml. **Les fichiers de configuration sont utilisés pour les suites personnalisées volumineuses et remplacent les paramètres par défaut de Tough Day 2. Les paramètres de ligne de commande remplacent les fichiers de configuration et les paramètres par défaut.**

La seule façon d’enregistrer une configuration de test consiste à la copier au format yaml.

### Ajout d’un test {#adding-a-new-test}

Si vous ne voulez pas utiliser la suite `toughday` par défaut, vous pouvez ajouter un test de votre choix en utilisant le paramètre `add`. Les exemples ci-dessous montrent comment ajouter le `CreateAssetTreeTest` testez en utilisant des paramètres de ligne de commande ou un fichier de configuration yaml.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Ajout de plusieurs instances du même test  {#adding-multiple-instances-of-the-same-test}

Vous pouvez également ajouter et exécuter plusieurs instances du même test, mais chaque instance doit avoir un nom unique. Les exemples ci-dessous montrent comment ajouter deux instances du même test à l’aide de paramètres de ligne de commande ou d’un fichier de configuration yaml.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

En utilisant un fichier de configuration yaml :

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

Si vous devez modifier une ou plusieurs propriétés de test, vous pouvez ajouter cette propriété à la ligne de commande ou au fichier de configuration yaml. Pour voir toutes les propriétés de test disponibles, ajoutez le paramètre `--help <TestClass/PublisherClass>` à la ligne de commande, par exemple :

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Gardez à l’esprit que les fichiers de configuration yaml remplaceront les paramètres par défaut de Tough Day 2 et que les paramètres de ligne de commande remplaceront les fichiers de configuration et les paramètres par défaut.

Les exemples ci-dessous montrent comment modifier la variable `template` pour la propriété `CreatePageTreeTest` testez en utilisant des paramètres de ligne de commande ou un fichier de configuration yaml.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Utilisation de suites de tests prédéfinies {#working-with-predefined-test-suites}

Les exemples ci-dessous montrent comment ajouter un test à une suite prédéfinie et reconfigurer et exclure un test existant d’une suite prédéfinie.

Vous pouvez ajouter un nouveau test à une suite prédéfinie en utilisant le paramètre `add` et en spécifiant la suite prédéfinie ciblée.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Les tests existants d’une suite donnée peuvent également être reconfigurés à l’aide du paramètre `config`. Vous devez également spécifier le nom de la suite et le nom réel du test (et non le nom de la classe de test). Le nom du test est disponible dans la propriété `name` de la classe de test. Pour savoir comment retrouver les propriétés de test, lisez la section [Modification des propriétés de test](/help/sites-developing/tough-day.md#changing-the-test-properties).

Dans l’exemple ci-dessous, le titre de la ressource par défaut pour `CreatePageTreeTest` (nommé `UploadAsset`) est remplacé par « NewAsset ».

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Vous pouvez également supprimer les tests des suites prédéfinies ou des éditeurs de la configuration par défaut à l’aide de l’option `exclude` . Vous devez également spécifier le nom de la suite et le nom réel du test (et non le test C). `lass` name). Le nom du test est disponible dans la propriété `name` de la classe de test. Dans l’exemple ci-dessous, le test `CreatePageTreeTest` (nommé `UploadAsset`) est supprimé de la suite toughday.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

En utilisant un fichier de configuration yaml :

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modes d’exécution {#run-modes}

Tough Day 2 peut fonctionner dans l’un des modes suivants : **normal** et **charge constante**.

Le mode d’exécution **normal** présente deux paramètres :

* `concurrency` : représente le nombre de threads que Tough Day 2 crée pour l’exécution du test. Sur ces threads, les tests sont exécutés jusqu’à ce que la durée soit écoulée ou qu’il n’y ait plus de tests à exécuter.

* `waittime` : temps d’attente entre deux exécutions de test consécutives sur le même thread. La valeur doit être exprimée en millisecondes.

L’exemple ci-dessous montre comment ajouter les paramètres à l’aide de la ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

ou en utilisant un fichier de configuration yaml :

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

Le mode d’exécution **charge constante** diffère du mode d’exécution normal dans la mesure où il génère un nombre constant d’exécutions de tests lancés, plutôt qu’un nombre constant de threads. Vous pouvez définir la charge en utilisant le paramètre du mode d’exécution du même nom.

### Sélection de test {#test-selection}

Le processus de sélection de test est le même pour les deux modes d’exécution et il se présente comme suit : tous les tests ont une propriété `weight` qui détermine la probabilité d’exécution dans un thread. Par exemple, si vous avez deux tests, l’un avec un poids de 5 et l’autre un poids de 10, le second est deux fois plus susceptible d’être exécuté que le premier.

De plus, les tests peuvent avoir une propriété `count`, ce qui limite le nombre d’exécutions à un nombre donné. Une fois ce nombre atteint, aucune autre exécution du test n’aura lieu. Toutes les instances de test en cours d’exécution se terminent selon leur configuration. L&#39;exemple suivant montre comment ajouter ces paramètres en ligne de commande ou à l&#39;aide d&#39;un fichier de configuration yaml.

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
En raison d’exécutions parallèles, le nombre réel d’exécutions de test ne correspond pas exactement à celui configuré dans le paramètre `count`. Attendez-vous à un écart proportionnel au nombre de threads simultanément en cours d’exécution (contrôlé par le `concurrency parameter`).

### Exécution d’essai {#dry-run}

Une exécution d’essai analyse toutes les entrées données (paramètres de ligne de commande ou fichiers de configuration), les fusionne avec les valeurs par défaut, puis génère les résultats. Il n’exécute aucun des tests.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Sortie {#output}

Tough Day 2 génère à la fois des métriques de test et des journaux. Pour plus de détails, lisez les sections suivantes.

### Mesures de test {#test-metrics}

Tough Day 2 signale actuellement neuf mesures de test que vous pouvez évaluer. Les mesures comportant le symbole **&#42;** sont générées uniquement si les exécutions ont réussi :

| **Nom** | **Description** |
|---|---|
| Timestamp | Horodatage de la dernière exécution de test terminée. |
| Réussite | Nombre d’exécutions réussies. |
| Échec | Nombre d’exécutions ayant échoué. |
| Min&#42; | Durée d’exécution de test la plus courte. |
| Max&#42; | Durée d’exécution de test la plus longue. |
| Médiane&#42; | Durée médiane calculée de toutes les exécutions de test. |
| Moyenne&#42; | Durée moyenne calculée de toutes les exécutions de test. |
| StdDev&#42; | Écart type. |
| 90p&#42; | 90e percentile |
| 99p&#42; | 99e percentile |
| 99.9p&#42; | 99,9e percentile |
| Débit réel&#42; | Nombre d’exécutions divisé par le temps d’exécution écoulé. |

Ces mesures sont écrites à l’aide d’éditeurs qui peuvent être ajoutés avec le paramètre `add` (comme pour l’ajout de tests). Actuellement, il existe deux options :

* **CSVPublisher** : émet un fichier CSV.
* **ConsolePublisher** : la sortie est affichée dans la console.

Par défaut, les deux éditeurs sont activés.

Il existe également deux modes dans lesquels les mesures sont signalées :

* Le mode de publication **simple** fait état des résultats depuis le début de l’exécution jusqu’au moment de leur publication.
* Le mode de publication **d’intervalle** publie les résultats selon un intervalle de temps donné. Vous pouvez définir cet intervalle avec le paramètre **interval** du mode de publication.

L’exemple suivant montre comment configurer le paramètre `intervals`au moyen de la ligne de commande ou d’un fichier de configuration yaml.

En utilisant les paramètres de ligne de commande :

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

En utilisant un fichier de configuration yaml :

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Journalisation {#logging}

Tough Day 2 crée un dossier .logs dans le répertoire où vous avez exécuté Tough Day 2. Ce dossier contient deux types de journaux :

* **toughday.log**: contient des messages liés à l’état de l’application, des informations de débogage et des messages globaux.
* **toughday_&lt;testname>.log**: messages liés au test spécifié.

Les journaux ne sont pas remplacés, les exécutions suivantes ajoutent des messages aux journaux existants. Les journaux ont plusieurs niveaux. Pour plus d’informations, consultez la section ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
