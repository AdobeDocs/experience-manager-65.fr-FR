---
title: '[!DNL Experience Manager Assets] de métadonnées C2PA'
description: Découvrez comment [!DNL Experience Manager Assets] détecte les métadonnées C2PA sur les ressources chargées, les signale dans l’interface utilisateur et signe les rendus qu’il génère pour les ressources IA dédiée à la génération .
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: f47205896ed512deadb4d31acbfe0fafa18515e7
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 6%
---

# Métadonnées C2PA dans [!DNL Experience Manager Assets] {#c2pa-metadata}

Les marques sont plus préoccupées que jamais par la transparence du contenu, la déclaration d’utilisation de l’IA et la prévention de l’altération des ressources. Le Content Authenticity Initiative (CAI) d’Adobe crée des outils conformes à la norme technique [C2PA](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) (Coalition for Content Provenance and Authenticity). Les métadonnées C2PA, un nouveau type de métadonnées inviolables, aident les visiteurs à comprendre la traçabilité du contenu et à garantir l’intégrité des ressources de la marque. Ils peuvent inclure un large éventail de données de provenance qui fournissent des informations dans l’historique d’une ressource numérique.

Cela inclut :

* **Émetteur ou signataire :** informations sur l’entité ou la société qui a émis la signature numérique de la ressource.
* **Date de l’événement :** date à laquelle les métadonnées C2PA ont été appliquées à la ressource.
* **Processus :** les enregistrements des modifications apportées à la ressource.
* **Détails de l’appareil :** informations sur l’application ou l’appareil utilisé pour créer ou modifier la ressource.
* **Outil d’IA utilisé :** si l’IA générative a été utilisée pour modifier ou créer la ressource, le nom du modèle utilisé est inclus.
* **Autres informations pertinentes :** données supplémentaires qui offrent plus de contexte sur l’historique d’une ressource.

Pour plus d’informations sur l’historique d’une ressource, voir [Vérifier](https://contentcredentials.org/verify).

[!DNL Adobe Experience Manager Assets] détecte les métadonnées C2PA lorsque vous chargez ou mettez à jour une ressource, signale ces ressources dans l’interface utilisateur [!DNL Assets] et conserve intacte la divulgation de l’IA dédiée aux générations sur les rendus générés par [!DNL Experience Manager]. Chaque fois que [!DNL Experience Manager] créez ou modifiez un rendu d’une ressource IA dédiée à la génération (miniature, rendu web, copie en filigrane ou transcode vidéo, par exemple), [!DNL Experience Manager] signe ce rendu avec une nouvelle métadonnée C2PA qui fait référence à la ressource d’origine en tant que son parent. Les rendus que vous téléchargez, publiez ou partagez conservent leur provenance.

## Conditions préalables {#Prerequisites}

La prise en charge des métadonnées C2PA nécessite le pack de services [!DNL Adobe Experience Manager] 6.5. Sur le pack de services 6.5.25.0, installez le correctif de conformité [AEM 6.5 SP25 - C2PA GenAI](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-ASSETS-75868-SP25-1.0.zip).

## Formats et plateformes pris en charge {#supported-formats}

### Formats {#formats}

[!DNL Experience Manager] signe les rendus dans les formats pris en charge par la spécification [C2PA](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) pour les manifestes incorporés.

| Type | Formats | Types MIME |
|---|---|---|
| Image | JPEG, PNG, GIF, TIFF, DNG, WebP, JPEG XL, AVIF, HEIC/HEIF, SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| Vidéo | MP4, MOV, AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| Audio | MP3, M4A, WAV, FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager] reconnaît également les alias courants, tels que `image/jpg`, `image/pjpeg`, `image/x-png` et `video/mov`. [!DNL Experience Manager] recherche un manifeste dans chaque ressource chargée, quel que soit le format de fichier. Les rendus dans d’autres formats, tels que PSD ou EPS, ne sont pas signés.

### Plateformes {#platforms}

La prise en charge des métadonnées C2PA repose sur un composant C2PA natif fourni dans le lot `cq-dam-core`, avec une version pour chaque plateforme prise en charge. Lorsque le service démarre, [!DNL Experience Manager] extrait la version de votre plateforme (`adobe_c2patool` ou `adobe_c2patool.exe` sous Windows) dans le dossier de données privées du lot, vérifie la somme de contrôle SHA-256 et l’exécute en tant que processus distinct. Vous n’avez pas besoin d’installer quoi que ce soit ni de modifier `PATH`.

| Système d’exploitation | Architecture |
|---|---|
| Linux (glibc 2.28 ou version ultérieure, y compris Red Hat Enterprise Linux 8) | `x86_64`, `aarch64` |
| Mac OS | `x86_64`, `aarch64` (silicium Apple) |
| Windows | `x86_64` |

Cela fonctionne de la même manière sur les déploiements [!DNL Adobe Managed Services] et sur site. Assurez-vous que le processus [!DNL Experience Manager] peut démarrer ce fichier exécutable. Si vous utilisez un logiciel de montage `noexec`, un antivirus ou un logiciel de sécurité de point d’entrée, autorisez `adobe_c2patool` à exécuter à partir du dossier `crx-quickstart`. Sinon, la prise en charge des métadonnées C2PA ne démarre pas.

## Fonctionnement des métadonnées C2PA {#how-c2pa-metadata-works}

La prise en charge des métadonnées C2PA comporte deux parties : la détection lorsqu’une ressource est chargée ou mise à jour et la signature à nouveau chaque fois que [!DNL Experience Manager] génère ou modifie un rendu.

### Configuration des workflows {#workflow}

L’étape **[!UICONTROL Détecter les informations d’identification C2PA]** affichée dans [Détecter les métadonnées C2PA](#detect) fait partie du modèle de workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** par défaut. Si vous utilisez une copie personnalisée de ce modèle, ajoutez l’étape vous-même :

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**, puis ouvrez votre modèle en ![icône Modifier](assets/edit.svg) **[!UICONTROL Modifier]** mode.
1. Ajoutez l’étape **[!UICONTROL Détecter les informations d’identification C2PA]** après **[!UICONTROL Processeur de métadonnées]**, avant qu’une étape ne génère les rendus.
1. Sélectionnez **[!UICONTROL Synchronisation]** pour enregistrer le modèle.

Les étapes de rendu ne signent leur sortie que si la détection a déjà été exécutée sur la ressource. Si la détection s’exécute après eux, leurs rendus restent sans signature jusqu’à ce que le workflow s’exécute à nouveau.

### Détection des métadonnées C2PA {#detect}

Le workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** comprend une étape **[!UICONTROL Détecter les informations d’identification C2PA]** qui s’exécute après l’étape **[!UICONTROL Processeur de métadonnées]** comme illustré dans la figure ci-dessous. Il lit le fichier binaire d’origine de la ressource et enregistre le résultat dans le nœud de métadonnées de la ressource `jcr:content/metadata`.

![Workflow](assets/workflow.png)

Le tableau suivant répertorie les propriétés de métadonnées clés dans le workflow de métadonnées C2PA.

| Propriété | Type | Description |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | `true`, si le fichier binaire d’origine comporte un manifeste C2PA incorporé. C&#39;est toujours écrit. |
| `dam:isAiGenerated` | `boolean` | `true`, si le manifeste place la ressource dans la portée de l’étiquetage IA dédiée à la génération. Il n’est écrit que lorsqu’un manifeste est présent. |
| `dam:c2paValidationState` | `string` | Il décrit l’état de validation du manifeste : `TRUSTED`, `VALID`, `INVALID` ou `UNKNOWN`. Il n’est écrit que lorsqu’un manifeste est présent. |

Lorsqu’un manifeste est présent, [!DNL Experience Manager] le stocke également comme rendu `c2pa-manifest.json` (`application/json`).

Si vous remplacez la ressource d’origine par un fichier binaire qui n’a pas de manifeste, l’exécution de workflow suivante définit `dam:hasC2PAManifest` sur `false` et supprime `dam:isAiGenerated`, `dam:c2paValidationState` et le rendu `c2pa-manifest.json`.

>[!NOTE]
>
>Un échec de détection ne bloque jamais l’ingestion d’une ressource. Si la lecture du manifeste expire ou échoue, [!DNL Experience Manager] consigne l’erreur, laisse les métadonnées inchangées et continue avec le reste du workflow.

### Affichage des métadonnées C2PA dans l’interface utilisateur [!DNL Assets] {#view-c2pa-metadata}

Les Assets qui transportent des métadonnées C2PA affichent le badge **cr** (métadonnées C2PA) dans l’interface utilisateur [!DNL Assets]. Accédez à **&#x200B;**&#x200B;> **[!UICONTROL Fichiers]** et recherchez le badge dans le coin inférieur gauche de :

* Miniature de la ressource en **[!UICONTROL mode Carte]**.
* Miniature de la ressource en mode **[!UICONTROL Colonnes]**. Sélectionnez la ressource pour afficher sa miniature.
* Zone d’aperçu de la page des détails de la ressource.

Le badge **cr** illustré dans la figure suivante indique si une ressource contient des métadonnées C2PA. Il n’affiche pas le manifeste lui-même. Pour afficher le manifeste complet, téléchargez la ressource et ouvrez-la dans [Vérifier](https://contentcredentials.org/verify).

![badge cr](assets/cr.png)

[!DNL Experience Manager] stocke le manifeste détecté comme rendu `c2pa-manifest.json` sur la ressource. Ce rendu est interne. Elle n’apparaît pas dans le panneau **[!UICONTROL Rendus]** de la page des détails de la ressource, ni dans le sélecteur de rendu.

### Signer les rendus {#sign-renditions}

Un rendu est un nouveau fichier binaire. Par conséquent, le manifeste incorporé dans la ressource d’origine ne le couvre pas. Pour conserver la divulgation de l’IA dédiée à la génération intacte, [!DNL Experience Manager] signe chaque rendu éligible comme la dernière étape du processus qui le produit. Les nouvelles métadonnées C2PA :

* Fait référence à la ressource d’origine en tant qu’ingrédient **parent**.
* Enregistre la manière dont le rendu a été dérivé de la ressource d’origine, dans le cadre de l’une des actions C2PA `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited`.
* Nomme `Adobe Experience Manager` l’agent logiciel.

[!DNL Experience Manager] signe un rendu uniquement lorsque tous les éléments suivants sont `true` :

* La ressource source a `dam:isAiGenerated` définie sur `true`. Les Assets qui contiennent un manifeste, mais qui ne sont pas générés via l’IA, affichent toujours le badge **cr**, mais [!DNL Experience Manager] ne signent pas à nouveau leurs rendus.
* Le manifeste source est lisible et son état de validation n&#39;est pas `INVALID`. [!DNL Experience Manager] n’enchaîne jamais une nouvelle signature sur un manifeste dont la validation a échoué, par exemple, après que la ressource a été falsifiée.
* Le format de rendu prend en charge un manifeste C2PA incorporé. Pour plus d’informations, voir [Formats pris en charge](#supported-formats). [!DNL Experience Manager] ignore les formats non pris en charge sans erreur.

Les étapes suivantes du workflow **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques terminée]** présentées dans [Détecter les métadonnées C2PA](#detect) signent leur sortie.

| Étape du workflow | Rendus signés | Action C2PA enregistrée |
|---|---|---|
| **[!UICONTROL Traiter les miniatures]** | Rendus de miniature et image web. | `c2pa.resized` et `c2pa.transcoded` lorsque le format change. |
| **[!UICONTROL Miniatures EPS (avec la technologie ImageMagick)]** | Sortie de Principal, miniatures dérivées et rendus web. | `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited` |
| **[!UICONTROL Miniatures FFmpeg]** | Images d’affiche et miniatures vidéo. | `c2pa.resized` et `c2pa.transcoded` |
| **[!UICONTROL Transcodage FFmpeg]** | Codages vidéo. | `c2pa.transcoded` |
| **[!UICONTROL Pixelliser le rendu d’aperçu d’image PDF/AI]** | Prévisualiser le rendu. (`cqdam.preview.png`) | `c2pa.transcoded` |

Les processus de workflow suivants signent également leur sortie lorsque vous les utilisez dans le workflow **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques terminée]** dans un autre workflow ou dans un modèle de workflow personnalisé. Sélectionnez-les dans la liste **[!UICONTROL Miniatures des processus]** d’une étape de workflow, comme indiqué dans [Détecter les métadonnées C2PA](#detect).

| Processus de workflow | Rendus signés | Action C2PA enregistrée |
|---|---|---|
| **[!UICONTROL Créer une miniature]** | Rendus de miniatures. | `c2pa.resized` et `c2pa.transcoded` lorsque le format change. |
| **[!UICONTROL Créer Une Image Web]** | Rendus Web. | `c2pa.resized` et `c2pa.transcoded` lorsque le format change. |
| **[!UICONTROL Ligne de commande]** par exemple, avec [!DNL ImageMagick] | Sortie de Principal, miniatures dérivées et rendus web. | `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited` |
| **[!UICONTROL Processus d’application d’un filigrane sur une image]** | Rendu avec filigrane ou rendu d’origine lorsque le filigrane est en place. Pour plus d’informations, voir [Filigrane de vos ressources](/help/assets/watermarking.md). | `c2pa.edited` |
| **[!UICONTROL Créer un Storyboard vidéo]** | Images clés du Storyboard. | `c2pa.transcoded` |
| **[!UICONTROL Écriture différée]** | Rendu d’origine une fois les métadonnées réécrites. Pour plus d’informations, voir [Écriture différée XMP dans les rendus](/help/assets/xmp-writeback.md). | `c2pa.edited` |

### Protéger le fichier binaire d’origine lors de l’écriture différée XMP {#xmp-writeback}

L’écriture différée XMP réécrit le fichier binaire d’origine, ce qui rompt son manifeste incorporé. Pour les ressources dont le `dam:hasC2PAManifest` est défini sur `true`, [!DNL Experience Manager] modifie le comportement de l’étape **[!UICONTROL Processus d’écriture différée XMP]** du workflow **[!UICONTROL Écriture différée des métadonnées de gestion des ressources numériques]** comme suit :

* **Ressources d’IA généralisées** (`dam:isAiGenerated` est `true`) : [!DNL Experience Manager] écrit le XMP, puis signe à nouveau le fichier binaire d’origine, avec le fichier binaire de pré-écriture comme parent. Cela permet d’enregistrer simultanément l’écriture différée et la nouvelle signature. Si la nouvelle signature échoue, les deux sont ignorés et l’étape échoue.
* **Autres ressources qui comportent un manifeste** : [!DNL Experience Manager] ignore l’écriture différée XMP et en consigne la raison. Le fichier binaire d’origine et son manifeste restent inchangés.

### Mode de signature {#signing-mode}

[!DNL Experience Manager] signe les rendus localement, sur l’instance qui les produit, avec un certificat éphémère et autosigné qu’il génère lui-même. La signature ne nécessite aucun accès réseau et aucune configuration de certificat ou de clé privée.

>[!NOTE]
>
>Vous ne pouvez pas configurer votre propre certificat de signature. Les programmes de validation tels que [Vérifier](https://contentcredentials.org/verify) affichent la divulgation de l’IA dédiée aux généralités du rendu et le lien vers l’original, mais n’identifient pas votre organisation en tant que signataire.

## Configuration des métadonnées C2PA {#configure}

La prise en charge des métadonnées C2PA est activée par défaut. Vous n’avez pas besoin d’installer ni de configurer quoi que ce soit.

### Configuration OSGi {#osgi-configuration}

Pour modifier la configuration par défaut, configurez le **[!UICONTROL service C2PA de gestion des ressources numériques Day CQ]** (`com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl` PID) dans le gestionnaire de configuration à l’adresse `https://[aem_server]:[port]/system/console/configMgr`comme illustré dans la figure ci-dessous) ou ajoutez une configuration OSGi à votre projet. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md).

![Configuration OSGi](assets/OSGi.png)

Le tableau ci-dessous répertorie les propriétés de la configuration OSGi de votre projet.

| Propriété | Nom dans Configuration Manager | Valeur par défaut | Description |
|---|---|---|---|
| `enabled` | **[!UICONTROL Activé]** | `true` | Active ou désactive la prise en charge des métadonnées C2PA. Lorsqu’elle est désactivée, [!DNL Experience Manager] ne détecte pas les manifestes et ne signe pas les rendus. |
| `timeoutMillis` | **[!UICONTROL Délai d’expiration de l’interface de ligne de commande (ms)]** | `30000` | Indique la durée maximale, en millisecondes, pendant laquelle [!DNL Experience Manager] attend une seule opération de lecture ou de signature sur un fichier avant de le traiter comme ayant expiré. Augmentez cette valeur pour les fichiers vidéo volumineux ou les fichiers image haute résolution. |

Par exemple, ajoutez une configuration OSGi à l’adresse `/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`.

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### Désactiver la prise en charge des métadonnées C2PA {#disable}

Dans la configuration du service C2PA de gestion des ressources numériques **[!UICONTROL Day CQ]** présentée dans la [configuration OSGi](#osgi-configuration), désactivez l’option **[!UICONTROL Activé]**, puis enregistrez les modifications. La modification prend effet immédiatement sans redémarrage :

* L’étape **[!UICONTROL Détecter les informations d’identification C2PA]** illustrée dans [Détecter les métadonnées C2PA](#detect) devient non opérationnelle.
* Les étapes de workflow créent des rendus sans les signer.
* Assets traité précédemment conserve sa propriété `dam:hasC2PAManifest` et affiche toujours le badge **cr**.

>[!CAUTION]
>
>Après avoir désactivé l’option **[!UICONTROL Activé]**, les rendus des ressources IA dédiée à la génération ne comportent aucune métadonnée C2PA. Si vous souhaitez vous conformer aux réglementations de divulgation de l’IA dédiée aux généralités, activez l’option **[!UICONTROL Activé]**.

## Personnalisation du pipeline de traitement {#customize}

Pour ajouter, supprimer ou réorganiser des étapes dans **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** tout en conservant la divulgation de l’IA dédiée aux généralités intacte, suivez ces règles :

* **Commencez par exécuter la détection.** Conservez **[!UICONTROL Détecter les informations d’identification C2PA]** avant chaque étape de création ou de modification des rendus.
* **Signer en dernier.** Toute modification apportée à un fichier binaire après la signature invalide sa signature. N’exécutez pas d’étapes qui modifient un rendu après l’étape qui l’a signé.
* **Utiliser des étapes de signature.** Les étapes intégrées répertoriées dans [Signer les rendus](#sign-renditions) signent leur sortie. Les étapes personnalisées et les outils tiers que vous exécutez par le biais d’un processus autre que le processus **[!UICONTROL Ligne de commande]** ne signent pas leur sortie, sauf si la signature est explicitement ajoutée. Pour plus d’informations, voir [Traitement des ressources à l’aide des workflows et des gestionnaires de médias](/help/assets/media-handlers.md).
* **Ne modifiez pas l’original en place** sauf si l’étape le signe à nouveau, comme le font **[!UICONTROL Écriture différée XMP]** et **[!UICONTROL Processus d’application d’un filigrane sur l’image]**.

### Signature de rendus à partir d’une étape de workflow personnalisé {#custom-step}

Les étapes de workflow personnalisées qui produisent des rendus peuvent les signer via le service OSGi `com.day.cq.dam.api.c2pa.C2PASigner`. Il applique les mêmes règles d’éligibilité que les étapes intégrées, mais fait état du résultat en tant que `C2PASigningOutcome` à la place.

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

Appelez `signIfEligible` uniquement une fois que votre étape a terminé d’écrire le rendu. Le service OSGi fournit les méthodes répertoriées dans le tableau ci-dessous.

| Méthode | Utilisez-le pour |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | Signez un nouveau rendu, avec la ressource source comme parent. |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | Signez plusieurs rendus dérivés de la même ressource. Cette méthode lit le manifeste source une fois. |
| `captureResignState(Asset)` | Prenez une image de la ressource d’origine avant que votre étape ne la modifie. Cette méthode renvoie `null` si la ressource n’est pas éligible. |
| `resign(Asset, Rendition, List<C2PAAction>)` | Resignez la ressource d’origine après une modification statique, avec l’image comme parent. |
| `discardResignState(Rendition)` | Placez une image que vous avez prise mais qui ne doit pas être utilisée, par exemple, car votre modification a échoué. |

Les valeurs de `C2PASigningOutcome` sont mentionnées dans le tableau ci-dessous.

| Résultat | Description |
|---|---|
| `SIGNED` | [!DNL Experience Manager] a signé le rendu. |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | La ressource source n’est pas marquée comme une ressource générée par l’IA. |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | Le format de rendu ne prend pas en charge le manifeste C2PA incorporé. |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager] n’a trouvé aucun manifeste sur la ressource source. |
| `SKIPPED_MANIFEST_NOT_VALID` | Échec de la validation du manifeste source. |
| `SKIPPED_SERVICE_UNAVAILABLE` | La prise en charge des métadonnées C2PA est désactivée ou indisponible. |
| `FAILED` | Échec de la lecture du manifeste source ou de la signature du rendu. |

Pour vérifier l’éligibilité avant de générer un rendu coûteux, appelez `C2PASupportedFormats.isEligible(...)`.

## Résolution des problèmes {#troubleshooting}

Lors de la résolution des problèmes, définissez les enregistreurs suivants sur `DEBUG` dans **[!UICONTROL Configuration de l’enregistreur de journalisation Apache Sling]**.

* `com.day.cq.dam.core.impl.c2pa` : extraction du composant C2PA natif, lectures de manifeste et signature.
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess` : détection.

| Symptôme | Cause possible | Résolution |
|---|---|---|
| Aucune ressource n’affiche le badge **cr**. | La prise en charge des métadonnées C2PA est désactivée ou votre modèle de workflow n’inclut pas l’étape de détection. | Vérifiez que la mention **[!UICONTROL Activé]** est activée dans la configuration **[!UICONTROL Service C2PA de gestion des ressources numériques Day CQ]** et que votre modèle **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** comprend **[!UICONTROL Détecter les informations d’identification C2PA]**. |
| Une ressource que vous connaissez possède un manifeste mais n’affiche aucun badge. | La ressource a été chargée avant que la fonctionnalité ne soit disponible. | Exécutez à nouveau le workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** sur la ressource, par exemple à partir de **[!UICONTROL Chronologie]** > **[!UICONTROL Démarrer le workflow]**. |
| Le service ne démarre pas. Le journal des erreurs signale que `adobe_c2patool` ne peut pas être extrait ni marqué comme exécutable. | Il n’existe aucun fichier binaire pour le système d’exploitation ou l’architecture, ou le système de fichiers bloque les exécutables. | Utilisez une plateforme prise en charge. Autorisez le processus [!DNL Experience Manager] à exécuter les fichiers exécutables à partir de leur dossier `crx-quickstart`. |
| Le journal des erreurs signale `GLIBC_2.xx not found`. | L’hôte Linux exécute une version de glibc antérieure à 2.28. | Mettez à niveau le système d’exploitation hôte. |
| La détection ou la signature a expiré. | Les fichiers volumineux prennent plus de temps que le délai d’expiration par défaut de 30 secondes. | Augmentez le délai d’expiration de l’interface **[!UICONTROL CLI (ms)]**. |
| Les rendus d’une ressource IA dédiée aux généralités ne sont pas signés. | Le format n’est pas pris en charge, le manifeste est `INVALID` ou la détection s’exécute après l’étape de rendu. | Cochez la `dam:c2paValidationState` et le format de rendu . Déplacez **[!UICONTROL Détecter les informations d’identification C2PA]** avant les étapes de rendu. |
| L’écriture différée XMP ne met pas à jour de ressource. | La ressource comporte un manifeste, mais n’est pas générée par l’intermédiaire de l’IA, de sorte que [!DNL Experience Manager] conserve son original inchangé. | Il s’agit d’un comportement attendu. Pour plus d’informations, voir [Protection de l’original lors de l’écriture différée XMP](#xmp-writeback). |

## Restrictions {#limitations}

* L’interface utilisateur [!DNL Assets] indique uniquement si des métadonnées C2PA sont présentes. Il n’a pas de panneau pour les détails du manifeste.
* [!DNL Experience Manager] signe à nouveau les rendus uniquement pour les ressources générées par l’IA. Les rendus d’autres ressources qui comportent un manifeste sont créés sans métadonnées C2PA.
* [!DNL Experience Manager] signe avec un certificat éphémère et autosigné. Les certificats de signature personnalisés ou spécifiques à une organisation ne sont pas pris en charge.


>[!MORELIKETHIS]
>
>* Métadonnées [C2PA dans la vue Assets de  [!DNL Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)
>* [Métadonnées C2PA dans  [!DNL Experience Manager Assets Essentials]](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/content-credentials)
>* [Métadonnées C2PA dans  [!DNL Dynamic Media]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)
>* [Écriture différée XMP sur les rendus](/help/assets/xmp-writeback.md)
>* [Ajoutez un filigrane à vos ressources](/help/assets/watermarking.md)
>* [&#128279;](https://contentauthenticity.org/)
>* [Vérifier](https://contentcredentials.org/verify)
