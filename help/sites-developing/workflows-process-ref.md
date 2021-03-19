---
title: Référence sur les processus de workflow
seo-title: Référence sur les processus de workflow
description: Référence sur les processus de workflow
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 84%

---


# Référence sur les processus de workflow{#workflow-process-reference}

AEM propose plusieurs étapes de processus qui peuvent être utilisées pour créer des modèles de workflow. Des étapes de processus personnalisées peuvent également être ajoutées pour les tâches qui ne sont pas couvertes par les étapes intégrées (voir [Création de modèles de workflow](/help/sites-developing/workflows-models.md)).

## Caractéristiques du processus {#process-characteristics}

Les caractéristiques suivantes sont décrites pour chaque étape du processus.

### Classe Java ou chemin d’accès ECMA  {#java-class-or-ecma-path}

Les étapes du processus sont définies soit par une classe Java soit par un ECMAScript.

* Dans le cas des processus de classe Java, un nom de classe complet est fourni.
* Pour les processus ECMAScript, le chemin d’accès au script est fourni.

### Charge utile  {#payload}

La charge utile est l’entité sur laquelle opère une instance de workflow. Elle est sélectionnée de manière implicite par le contexte dans lequel une instance de workflow est lancée.

Par exemple, si un workflow est appliqué à une page AEM *P*, *P* passe d’une étape à l’autre à mesure que le workflow est exécuté ; chaque étape pouvant éventuellement agir sur·*P* dans une certaine mesure.

Dans le cas le plus courant, la charge utile est un nœud JCR du référentiel (une ressource ou une page AEM, par exemple). Une charge utile Nœud JCR est transmise sous la forme d’une chaîne qui est soit un chemin d’accès JCR, soit un identifiant JCR (UUID). Dans certains cas, la charge utile peut être une propriété JCR (transmise en tant que chemin d’accès JCR), une URL, un objet binaire ou un objet Java générique. Les différentes étapes du processus qui agissent effectivement sur la charge utile attendent généralement une charge utile d’un certain type ou se comportent différemment selon le type de charge. Le type de charge utile attendu, le cas échéant, est décrit pour chaque processus présenté ci-dessous.

### Arguments  {#arguments}

Certains processus de workflow acceptent les arguments spécifiés par l’administrateur lors de la configuration de l’étape de workflow.

Les arguments sont saisis sous la forme d’une chaîne unique dans la propriété **Arguments du processus** du volet **Propriétés** de l’éditeur de workflow. Pour chaque processus décrit ci-dessous, le format de la chaîne d’arguments est décrit dans une grammaire EBNF simple. Par exemple, l’exemple suivant indique que la chaîne d’arguments est composée d’une ou de plusieurs paires séparées par des virgules, où chaque paire se compose d’un nom (chaîne) et d’une valeur, séparés par un deux-points doublon :

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Délai dépassé {#timeout}

Une fois ce délai d’expiration dépassé, l’étape de workflow n’est plus opérationnelle. Certains processus de workflow respectent le délai d’expiration, tandis que d’autres l’ignorent.

### Autorisations {#permissions}

La session transmise à `WorkflowProcess` est soutenue par l’utilisateur du service pour le service de processus de flux de travail, qui dispose des autorisations suivantes à la racine du référentiel :

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Si cet ensemble d&#39;autorisations n&#39;est pas suffisant pour votre implémentation `WorkflowProcess`, il doit alors utiliser une session avec les autorisations requises.

La méthode recommandée consiste à employer un utilisateur de service créé avec le sous-ensemble minimum d’autorisations requises.

>[!CAUTION]
>
>Si vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.2, la mise à jour de votre implémentation peut s’avérer nécessaire.
>
>Dans les versions précédentes, la session administrateur était transmise aux implémentations `WorkflowProcess` et pouvait alors bénéficier d’un accès complet au référentiel, sans devoir définir de listes de contrôle d’accès (ACL) spécifiques.
>
>Les autorisations sont désormais définies comme ci-dessus ([Autorisations](#permissions)). Il en va de même pour la méthode recommandée pour la mise à jour de votre implémentation.
>
>Une solution à court terme est également disponible à des fins de rétrocompatibilité lorsque des modifications de code ne sont pas possibles :
>
>* À l&#39;aide de la console Web ( `/system/console/configMgr` localisez le **service de configuration du processus de granite d&#39;Adobe**
   >
   >
* Activez le **mode hérité du processus de workflow**.
>
>
Vous revenez alors au comportement précédent qui fournissait une session administrateur à l’implémentation `WorkflowProcess` et disposez à nouveau d’un accès illimité à l’intégralité du référentiel.

## Processus de contrôle du workflow {#workflow-control-processes}

Les processus suivants n’exécutent aucune action sur le contenu. Ils servent à contrôler le comportement du workflow proprement dit.

### AbsoluteTimeAutoAdvancer (Avance automatique temps absolu écoulé) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Le processus `AbsoluteTimeAutoAdvancer` (Avance automatique temps absolu écoulé) se comporte de la même manière que **AutoAdvancer** (Avance automatique), si ce n’est qu’il arrive à expiration à une date et une heure données, plutôt qu’après une durée définie.

* **Classe** Java :  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Charge utile** : aucune.
* **Arguments** : aucun.
* **Délai d’expiration** : le processus arrive à expiration lorsque la date et l’heure définies sont atteintes.

### AutoAdvancer (Avance automatique) {#autoadvancer-auto-advancer}

Le processus `AutoAdvancer` fait passer automatiquement le flux de travail à l’étape suivante. Si plusieurs étapes sont possibles (il existe, par exemple, une division OU), la progression du flux de travail continue le long de l’*itinéraire par défaut*, si cela a été défini. Dans le cas contraire, aucune avance n’est effectuée.

* **Classe** Java :  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Charge utile** : aucune.
* **Arguments** : aucun.
* **Délai d’expiration** : le processus arrive à expiration après une durée définie.

### ProcessAssembler (Programme d’assemblage des processus) {#processassembler-process-assembler}

Le processus `ProcessAssembler` exécute plusieurs sous-processus de manière séquentielle au cours d’une seule étape. Pour utiliser le processus `ProcessAssembler`, créez une seule étape de ce type dans votre workflow, et configurez ses arguments de manière à indiquer les noms et arguments des sous-processus que vous souhaitez exécuter.

* **Classe** Java :  `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Charge utile** : ressource DAM, page AEM ou aucune charge utile (cela dépend des exigences des sous-processus).
* **Arguments** :

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Délai d’expiration** : respecté.

Par exemple :

* Extrayez les métadonnées de la ressource.
* Créez trois miniatures des trois tailles spécifiées.
* Créez une image JPEG à partir de la ressource, en supposant que la ressource d’origine n’est ni au format GIF ni au format PNG (auquel cas aucune image JPEG n’est créée).
* Définissez la date de la dernière modification de la ressource.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Processus de base {#basic-processes}

Les processus suivants exécutent des tâches simples ou servent simplement d’exemples.

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé lors de la prochaine mise à niveau de votre instance (et peut être remplacé lorsque vous appliquez un correctif logiciel ou un pack de fonctionnalités).

### Supprimez {#delete}

L’élément situé à l’emplacement indiqué est supprimé.

* **Chemin** ECMAScript :  `/libs/workflow/scripts/delete.ecma`

* **Charge utile** : chemin JCR
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### noop {#noop}

Il s’agit d’un processus nul. Il n’effectue aucune opération, mais consigne un message de débogage.

* **Chemin** ECMAScript :  `/libs/workflow/scripts/noop.ecma`

* **Charge utile** : aucune
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### rule-false {#rule-false}

Il s’agit d’un processus nul qui renvoie `false` sur la méthode `check()`.

* **Chemin** ECMAScript :  `/libs/workflow/scripts/rule-false.ecma`

* **Charge utile** : aucune
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### sample {#sample}

Il s’agit d’un exemple de processus ECMAScript.

* **Chemin** ECMAScript :  `/libs/workflow/scripts/sample.ecma`

* **Charge utile** : aucune
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### urlcaller {#urlcaller}

Il s’agit d’un processus de workflow simple qui appelle l’URL indiquée. En règle générale, l’URL est une référence à un JSP (ou à un autre servlet équivalent) qui effectue une tâche simple. Ce processus doit uniquement être utilisé pendant les phases de développement et de démonstration, mais pas dans un environnement de production. Les arguments définissent l’URL, le nom de connexion et le mot de passe.

* **Chemin** ECMAScript :  `/libs/workflow/scripts/urlcaller.ecma`

* **Charge utile** : aucune
* **Arguments** :

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

Par exemple : `http://localhost:4502/my.jsp, mylogin, mypassword`

* **Délai d’expiration** : ignoré

### LockProcess {#lockprocess}

Verrouille la charge utile du workflow.

* **Classe Java:** `com.day.cq.workflow.impl.process.LockProcess`

* **Charge utile :** JCR_PATH et JCR_UUID
* **Arguments** : aucun
* **Délai d’expiration** : ignoré.

L’étape n’a aucun effet dans les cas suivants :

* La charge utile est déjà verrouillée
* Le nœud de charge utile ne comporte pas de contenu enfant jcr:content

### UnlockProcess {#unlockprocess}

Déverrouille la charge utile du workflow.

* **Classe Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Charge utile :** JCR_PATH et JCR_UUID
* **Arguments** : aucun
* **Délai d’expiration** : ignoré.

L’étape n’a aucun effet dans les cas suivants :

* La charge utile est déjà déverrouillée
* Le nœud de charge utile ne comporte pas de contenu enfant jcr:content

## Processus de création de versions {#versioning-processes}

Le processus suivant effectue une tâche relative à la version.

### CreateVersionProcess  {#createversionprocess}

Crée une version de la charge utile du workflow (page AEM ou ressource DAM).

* **Classe Java**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Charge utile** : chemin JCR ou UUIF faisant référence à une page ou une ressource DAM
* **Arguments** : aucun
* **Délai d’expiration** : respecté

