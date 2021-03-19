---
title: AEM Mobile – Préparation pour le RGPD
seo-title: AEM Mobile – Préparation pour le RGPD
description: '"AEM Mobile – Préparation pour le RGPD"'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 84%

---


# AEM Mobile – Préparation pour le RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations relatives à la protection des données et à la protection de la vie privée ; comme le RGPD, l&#39;ACCP, etc.

## Prise en charge du RGPD par AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile est prêt à aider les clients avec les obligations de conformité au RGPD. Aucune donnée personnelle n’est stockée dans AEM Mobile. Si vous avez accès, vous pouvez vous connecter à Adobe Experience Mobile à l’aide de votre Adobe ID.

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Le produit de publication digitale d’Adobe (qui précède AEM Mobile) prend en charge les initiatives d’Adobe pour se préparer au RGPD. Voir [https://www.adobe.com/fr/privacy/general-data-protection-regulation.html](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html). Vous trouverez ci-dessous des explications sur la prise en charge des fonctions associées au RGPD dans le produit Digital Publishing Suite, notamment sur la façon de travailler avec Adobe afin de présenter des demandes RGPD.

Pour vous assurer de ne pas confondre AEM Mobile avec l’ancien produit Digital Publishing Suite, vous pouvez vous connecter au produit Digital Publishing Suite ici :

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### Présentation d’une demande RGPD {#initiating-a-gdpr-request}

Veuillez contacter l’assistance clientèle d’Adobe afin de présenter une demande RGPD pour Digital Publishing Suite.

Les identifiants suivants sont requis pour localiser les données du client. Tout sous-ensemble reçu impliquera que les autres identifiants ne s’appliquaient pas à cet utilisateur.

Obligatoire:

* Identifiant du contrat du client : *dpsc-contractId*

Fournissez au moins une des informations suivantes :

* L’identifiant OAuth de l’utilisateur final fourni par le client (l’identifiant utilisé dans le système de droits direct du client) : *dpsc-directEntitlementId*
* Pour les utilisateurs d’applications Windows, l’ID de la boutique d’applications de l’utilisateur final : *dpsc-windowsAppStoreId*
* L’adresse électronique de utilisateur final utilisée pour interagir avec l’application DPS : *email*

### Questions fréquentes (FAQ) {#frequently-asked-questions-faq}

**L’Adobe va-t-il supprimer mes achats de boutique d’applications lors du lancement d’une demande de DELETE ?**

Adobe supprime les informations qu’il contient au sujet des achats dans les boutiques d’applications (abonnements, etc.), mais les achats resteront enregistrés dans les boutiques d’applications. Si l’application (pour l’utilisateur final) est consignée dans la boutique d’applications, ces reçus seront à nouveau détectés et envoyés à Adobe ; ils seront considérés comme de nouveaux achats et restaurés par l’application afin d’en rétablir l’accès.

**L&#39;Adobe va-t-il supprimer les droits fournis par le client lors du lancement d&#39;une demande de DELETE ?**

Adobe supprimera les informations dont il dispose sur les droits directs supplémentaires du client. Si l’application (pour l’utilisateur final) se connecte au mécanisme OAuth que le client a utilisé, des informations seront envoyées à Adobe, et les services détecteront à nouveau les droits supplémentaires.

**À quoi s&#39;attend l&#39;utilisateur final ?**

Étant donné que la clé d’attribution des droits de l’application réside sur l’appareil en tant que partie intégrante du logiciel de visionneuse, l’utilisateur final doit désinstaller l’application. L’utilisateur final doit se rendre compte que s’il réinstalle l’application, les achats existants (associés à un utilisateur de la boutique d’applications) et les droits directs (associés à l’utilisateur OAuth) seront toujours restaurés.

**Que se passe-t-il lorsqu’une application est partagée entre des personnes sur un appareil ?**

Adobe dispose de très peu d’informations associées directement à un utilisateur spécifique. Il associe les données à l’aide d’un UUID créé de manière aléatoire et conservé dans les données de l’application qui est transmis dans chaque demande effectuée par l’application. Cela signifie que les utilisateurs finaux partageant l’application sur le même appareil utilisent le même UUID et que toutes les données sont considérées comme étant détenues par la personne à l’origine de la demande RGPD. Pour les demandes d’accès et de suppression, DPSC considère les personnes qui partagent une application comme une seule et même personne.

**Quelles sont les données personnelles suivies avec Analytics ?**

Aucune. Des données sont suivies, mais au niveau de l’application (et pas au niveau personnel). Il s’agit notamment des événements comme les lancements, les blocages, les fermetures, les activités, les achats ou les incrustations de folio. Les emplacements géographiques, les noms, les ID d’appareils et les adresses IP ne sont pas suivis.

**L’utilisateur final a fourni ses informations, mais rien n’a été trouvé. Pourquoi pas ?**

Au fil de l’évolution du produit Digital Publishing Suite, les mises en œuvre de services ont été modifiées, et davantage de données ont été obscurcies. Si aucune donnée n’a été trouvée en utilisant les données fournies par l’utilisateur, cela signifie que les données utilisateur ne permettent pas d’identifier cette personne.

### Exemple {#example}

Veuillez contacter l’assistance clientèle d’Adobe pour présenter une demande RGPD.

Voici un exemple des entrées et des sorties résultantes d’une demande de RDPR Digital Publishing Suite :

#### Entrées : {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### Sorties {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

