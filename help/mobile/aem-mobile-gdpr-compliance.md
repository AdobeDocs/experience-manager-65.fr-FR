---
title: Adobe Experience Manager Mobile - Préparation au RGPD
description: Adobe Experience Manager Mobile - Préparation au RGPD
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 5%

---

# AEM Mobile - Préparation au RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité, comme le RGPD, le CCPA, etc.

## Prise en charge du RGPD pour AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile est prêt à aider les clients à respecter le RGPD. Aucune donnée personnelle n’est stockée dans AEM Mobile. Si les privilèges d’accès vous permettent de vous connecter à Adobe Experience Mobile avec votre Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Le produit de publication numérique d’Adobe (qui précède AEM Mobile) prend en charge les initiatives de préparation au RGPD de l’Adobe. Veuillez consulter [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html). Vous trouverez ci-dessous des informations spécifiques sur la prise en charge des fonctions relatives au RGPD dans le produit Digital Publishing Suite, notamment sur la manière d’utiliser Adobe pour lancer des demandes en vertu du RGPD.

Pour vous assurer de ne pas confondre AEM Mobile avec l’ancien produit Digital Publishing Suite, vous pouvez vous connecter au produit Digital Publishing Suite à l’adresse suivante :

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Lancement d’une demande en vertu du RGPD {#initiating-a-gdpr-request}

Contactez l’assistance clientèle d’Adobe pour lancer une demande en vertu du RGPD pour Digital Publishing Suite.

Les identifiants suivants sont requis pour localiser les données client. Tout sous-ensemble reçu impliquera que les autres identifiants ne s’appliquaient pas à cet utilisateur.

Obligatoire:

* ID de contrat du client : *dpsc-contractId*

Fournissez au moins l’une des informations suivantes :

* L’identifiant OAuth fourni par le client final (l’identifiant utilisé dans le système de droits directs du client) : *dpsc-directEntitlementId*
* Pour les utilisateurs de l’application Windows, l’App Store ID de l’utilisateur final : *dpsc-windowsAppStoreId*
* Adresse électronique de l’utilisateur final utilisée pour interagir avec l’application DPS : *email*

### Questions fréquentes {#frequently-asked-questions-faq}

**Adobe supprimera-t-il mes achats App Store lors du lancement d’une demande de DELETE ?**

Adobe supprime les informations qu’il possède sur les achats de la boutique d’applications (abonnements, etc.) mais les achats seront toujours enregistrés dans les boutiques d’applications. Si l’application (utilisateur final) est connectée à la boutique d’applications, ces accusés de réception sont à nouveau récupérés et envoyés à l’Adobe. Par la suite, ils seront considérés comme de nouveaux achats et seront restaurés par l’application pour y avoir à nouveau accès.

**Adobe supprimera-t-il les droits fournis par les clients lors de la présentation d’une demande de DELETE ?**

Adobe supprimera les informations qu’il détient sur les droits directs supplémentaires du client. Si l’application (utilisateur final) se connecte au mécanisme OAuth utilisé par le client, il envoie des informations à Adobe et les services récupèrent les droits supplémentaires.

**Que doit-on attendre de l’utilisateur final ?**

Puisque la clé d’attribution des droits à l’application réside sur l’appareil dans le cadre du logiciel de visionneuse, l’utilisateur final doit désinstaller l’application. L’utilisateur final doit comprendre que s’il réinstalle l’application, les achats existants (associés à l’utilisateur de la boutique d’applications) et les droits directs (associés à l’utilisateur OAuth du client) seront toujours restaurés.

**Que se passe-t-il lorsqu’une application est partagée entre des personnes sur un appareil ?**

Adobe ne contient que très peu d’informations qui s’associent directement à un utilisateur spécifique. Il associe les données à l’aide d’un UUID créé de manière aléatoire et conservé dans les données de l’application, qui est transmis dans chaque requête initiée par l’application. Cela signifie que les utilisateurs finaux partageant l’application sur le même appareil utiliseront le même UUID et que toutes les données seront considérées comme appartenant à la personne qui émet la demande en vertu du RGPD. Pour les demandes d’accès et de suppression, le DPSC considère les personnes qui partagent une application comme une seule personne.

**Quelles sont les données personnelles suivies avec Analytics ?**

Aucune. Des données font l’objet d’un suivi, mais elles se trouvent au niveau de l’application (et non au niveau personnel). Cela inclut les événements tels que les lancements, les blocages, les fermetures, les activités, les achats ou les incrustations de folios. Les emplacements géographiques, les noms, les identifiants d’appareil ou les adresses IP ne sont pas suivis.

**L&#39;utilisateur final a fourni ses informations mais rien n&#39;a été trouvé. Pourquoi pas ?**

Au fur et à mesure de l’évolution du produit Digital Publishing Suite, les mises en oeuvre des services ont été modifiées et davantage de données ont été obscurcies. Si aucune donnée n’a été trouvée à l’aide des données fournies par l’utilisateur, cela signifie que les données de l’utilisateur ne peuvent pas être suivies à nouveau pour cette personne.

### Exemple {#example}

Veuillez contacter l’assistance clientèle d’Adobe pour lancer une demande en vertu du RGPD.

Voici un exemple des entrées et des sorties résultantes d’une demande en vertu du RGPD pour Digital Publishing Suite :

#### Entrées : {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
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
