---
title: Référence sur les processus de workflow
description: Référence sur les processus de workflow
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 38%

---

# Référence sur les processus de workflow{#workflow-process-reference}

AEM fournit plusieurs étapes de processus qui peuvent être utilisées pour créer des modèles de workflow. Des étapes de processus personnalisées peuvent également être ajoutées pour les tâches qui ne sont pas couvertes par les étapes intégrées (voir [Création de modèles de processus](/help/sites-developing/workflows-models.md)).

## Caractéristiques du processus {#process-characteristics}

Pour chaque étape du processus, les caractéristiques suivantes sont décrites.

### Classe Java™ ou chemin d’accès ECMA {#java-class-or-ecma-path}

Les étapes du processus sont définies par une classe Java™ ou un ECMAScript.

* Pour les processus de classe Java™, le nom de classe complet est fourni.
* Pour les processus ECMAScript, le chemin d’accès au script est fourni.

### Payload {#payload}

La charge utile est l’entité sur laquelle agit une instance de workflow. La payload est sélectionnée implicitement par le contexte dans lequel une instance de workflow est démarrée.

Par exemple, si un workflow est appliqué à une page AEM *P*, *P* passe d’une étape à l’autre à mesure que le workflow est exécuté ; chaque étape pouvant éventuellement agir sur *P* dans une certaine mesure.

Dans le cas le plus courant, la charge utile est un noeud JCR dans le référentiel (par exemple, une page AEM ou une ressource). Un payload de noeud JCR est transmis sous la forme d’une chaîne correspondant à un chemin JCR ou à un identifiant JCR (UUID). Parfois, la charge utile peut être une propriété JCR (transmise comme un chemin JCR), une URL, un objet binaire ou un objet Java™ générique. Les étapes de processus individuelles qui agissent effectivement sur la payload s’attendent généralement à une payload d’un certain type, ou agissent différemment selon le type de payload. Pour chaque processus décrit ci-dessous, le type de charge utile attendu, le cas échéant, est décrit.

### Arguments {#arguments}

Certains processus de workflow acceptent les arguments que l’administrateur spécifie lors de la configuration de l’étape du processus.

Les arguments sont saisis sous la forme d’une seule chaîne dans la variable **Arguments de processus** dans la propriété **Propriétés** du volet de l’éditeur de workflow. Pour chaque processus décrit ci-dessous, le format de la chaîne d’argument est décrit dans une grammaire EBNF simple. Par exemple, le code suivant indique que la chaîne d’argument est composée d’une ou de plusieurs paires délimitées par des virgules, où chaque paire se compose d’un nom (qui est une chaîne) et d’une valeur, séparés par un deux-points :

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Expiration {#timeout}

Après ce délai d’expiration, l’étape du workflow n’est plus opérationnelle. Certains processus de workflow respectent le délai d’expiration, tandis que d’autres ne l’appliquent pas et sont ignorés.

### Autorisations {#permissions}

La session transmise à `WorkflowProcess` est gérée par l’utilisateur pour le service de processus de workflow, avec les autorisations suivantes au niveau de la racine du référentiel :

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Si cet ensemble d’autorisations s’avère insuffisant pour votre implémentation de `WorkflowProcess`, elle doit utiliser une session avec les autorisations requises.

La méthode recommandée consiste à utiliser un utilisateur de service créé avec le sous-ensemble d’autorisations requis nécessaire, mais minimal.

>[!CAUTION]
>
>Si vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.2, vous devrez peut-être mettre à jour votre mise en oeuvre.
>
>Dans les versions précédentes, la session d’administration était transmise à la `WorkflowProcess` Les mises en oeuvre et peuvent alors disposer d’un accès complet au référentiel sans avoir à définir des listes de contrôle d’accès spécifiques.
>
>Les autorisations sont désormais définies comme ci-dessus ([Autorisations](#permissions)). Comme est la méthode recommandée pour mettre à jour votre mise en oeuvre.
>
>Une solution à court terme est également disponible à des fins de rétrocompatibilité lorsque des modifications de code ne sont pas possibles :
>
>* À l’aide de la console web (`/system/console/configMgr`, recherchez le **service de configuration de workflow Adobe Granite**.
>
>* Activez le **mode hérité du processus de workflow**.
>
>Cela revient à l’ancien comportement consistant à fournir une session d’administrateur à la `WorkflowProcess` et permettre un accès illimité à l’ensemble du référentiel une fois de plus.

## Processus de contrôle des workflows {#workflow-control-processes}

Les processus suivants n’effectuent aucune action sur le contenu. Ils servent à contrôler le comportement du workflow proprement dit.

### AbsoluteTimeAutoAdvancer (Avance automatique temps absolu écoulé) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Le processus `AbsoluteTimeAutoAdvancer` (Avance automatique temps absolu écoulé) se comporte de la même manière que l’**AutoAdvancer**, si ce n’est qu’il arrive à expiration à une date et une heure données, plutôt qu’après une durée définie.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Payload** : aucune.
* **Arguments** : aucun.
* **Délai d’expiration** : le processus arrive à expiration lorsque la date et l’heure définies sont atteintes.

### AutoAdvancer (Avance automatique) {#autoadvancer-auto-advancer}

Le processus `AutoAdvancer` fait passer automatiquement le workflow à l’étape suivante. Si plusieurs étapes sont possibles (il existe, par exemple, une division OU), la progression du workflow continue le long de l’*itinéraire par défaut*, si cela a été défini. Dans le cas contraire, aucune avance n’est effectuée.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Payload** : aucune.
* **Arguments** : aucun.
* **Délai d’expiration** : le processus arrive à expiration après une durée définie.

### ProcessAssembler (Programme d’assemblage des processus) {#processassembler-process-assembler}

Le `ProcessAssembler` Le processus exécute plusieurs processus secondaires de manière séquentielle dans une seule étape du processus. Pour utiliser la variable `ProcessAssembler`, créez une seule étape de ce type dans votre workflow et définissez ses arguments pour indiquer les noms et arguments des sous-processus que vous souhaitez exécuter.

* **Classe Java™**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Payload**: Ressource de gestion des actifs numériques, AEM page ou aucune charge utile (dépend des exigences des sous-processus).
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
* Créez une image de JPEG à partir de la ressource, en supposant que la ressource n’est à l’origine pas un GIF ou un fichier PNG (auquel cas aucun JPEG n’est créé).
* Définissez la date de dernière modification sur la ressource.

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
>Vous ne devez rien modifier dans le chemin `/libs`.
>
>Cela est dû au fait que le contenu de `/libs` sera écrasé la prochaine fois que vous mettrez à niveau votre instance (et éventuellement lors de l’application d’un correctif logiciel ou d’un pack de fonctionnalités).

### delete {#delete}

L’élément du chemin d’accès donné est supprimé.

* **Chemin ECMAScript** : `/libs/workflow/scripts/delete.ecma`

* **Payload** : chemin JCR
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### noop {#noop}

Il s’agit du processus nul. Il n’effectue aucune opération, mais consigne un message de débogage.

* **Chemin ECMAScript** : `/libs/workflow/scripts/noop.ecma`

* **Payload** : aucun
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### rule-false {#rule-false}

Il s’agit d’un processus nul qui renvoie `false` sur la méthode `check()`.

* **Chemin ECMAScript** : `/libs/workflow/scripts/rule-false.ecma`

* **Payload** : aucun
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### sample {#sample}

Voici un exemple de processus ECMAScript.

* **Chemin ECMAScript** : `/libs/workflow/scripts/sample.ecma`

* **Payload** : aucun
* **Arguments** : aucun
* **Délai d’expiration** : ignoré

### LockProcess {#lockprocess}

Verrouille la charge utile du workflow.

* **Classe Java™ :** `com.day.cq.workflow.impl.process.LockProcess`

* **Payload** : JCR_PATH et JCR_UUID
* **Arguments :** Aucun
* **Timeout :** Ignoré

L’étape n’a aucun effet dans les cas suivants :

* Le payload est déjà verrouillé.
* Le nœud de payload ne comporte pas de contenu enfant jcr:content.

### UnlockProcess {#unlockprocess}

Déverrouille la charge utile du workflow.

* **Classe Java™ :** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Payload** : JCR_PATH et JCR_UUID
* **Arguments :** Aucun
* **Timeout :** Ignoré

L’étape n’a aucun effet dans les cas suivants :

* Le payload est déjà déverrouillé.
* Le nœud de payload ne comporte pas de contenu enfant jcr:content.

## Processus de contrôle de version {#versioning-processes}

Le processus suivant effectue une tâche liée aux versions.

### CreateVersionProcess {#createversionprocess}

Crée une version de la charge utile de workflow (AEM page ou ressource DAM).

* **Classe Java™**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Payload** : chemin JCR ou UUID faisant référence à une page ou une ressource de gestion des ressources numériques
* **Arguments** : aucun
* **Délai d’expiration** : respecté
