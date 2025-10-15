---
title: Adobe Experience Manager Mobile - Préparation pour le RGPD
description: Découvrez comment Adobe Experience Manager est prêt à vous aider à respecter vos obligations de conformité au RGPD.
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# AEM Mobile - Préparation pour le RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité, comme le RGPD et le CCPA.

{{ue-over-mobile}}

## Prise en charge du RGPD par AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile est prêt à aider les clients avec leurs obligations de conformité au RGPD. Aucune donnée personnelle n’est stockée dans AEM Mobile. Si vous disposez des privilèges d’accès, vous pouvez vous connecter à Adobe Experience Mobile avec votre Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Le produit de publication numérique d’Adobe (qui précède AEM Mobile) prend en charge les initiatives de préparation d’Adobe au RGPD. Voir [https://business.adobe.com/fr/privacy/general-data-protection-regulation.html](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html). Vous trouverez ci-dessous des informations détaillées sur la prise en charge des fonctions relatives au RGPD dans le produit Digital Publishing Suite, y compris sur la manière de travailler avec l’Adobe pour lancer des demandes RGPD.

Pour vous assurer de ne pas confondre AEM Mobile avec l’ancien produit de Digital Publishing Suite, vous pouvez vous connecter au produit de Digital Publishing Suite ici :

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Lancement d’une requête RGPD {#initiating-a-gdpr-request}

Contactez l’assistance clientèle d’Adobe afin de pouvoir envoyer une demande RGPD pour le Digital Publishing Suite.

Les identifiants suivants sont requis pour localiser les données client. Tout sous-ensemble reçu implique que les autres ID ne s’appliquaient pas à cet utilisateur.

Obligatoire :

* ID de contrat du client : *dpsc-ContractId*

Fournissez au moins 1 des éléments suivants :

* L’ID OAuth fourni par le client ou la cliente final(e) (l’ID utilisé dans le système de droits directs du client ou de la cliente) : *dpsc-directEntitlementId*
* Pour les utilisateurs de l’application Windows, l’identifiant App Store de l’utilisateur final : *dpsc-windowsAppStoreId*
* Adresse e-mail utilisée par l’utilisateur final pour interagir avec l’application DPS : *e-mail*

### Questions fréquentes {#frequently-asked-questions-faq}

**L’Adobe est-il en train de supprimer mes achats App Store lors du lancement d’une demande de DELETE ?**

L’Adobe supprime les informations dont il dispose sur les achats effectués dans l’App Store (abonnements, etc.), mais les achats sont toujours enregistrés dans l’App Store. Si l’application (utilisateur final) est connectée à l’App Store, ces reçus sont à nouveau récupérés et envoyés à l’Adobe. Par la suite, ils sont considérés comme de nouveaux achats et sont restaurés par l’application, avec un nouvel accès.

**L’Adobe supprime-t-il les droits fournis par le client lors du lancement d’une demande de DELETE ?**

L’Adobe supprime les informations dont il dispose sur les droits directs supplémentaires du client. Si l’application (utilisateur final) se connecte au mécanisme OAuth que le client a utilisé, elle envoie des informations à l’Adobe et les services récupèrent à nouveau les droits supplémentaires.

**Qu’attend-on de l’utilisateur final ?**

Comme la clé d’attribution des droits à l’application réside sur l’appareil dans le cadre du logiciel de la visionneuse, l’utilisateur final doit désinstaller l’application. L’utilisateur final doit réaliser que s’il réinstalle l’application, les achats existants (associés à l’utilisateur de la boutique d’applications) et les droits d’utilisation directs (associés à l’utilisateur OAuth du client) sont toujours restaurés.

**Que se passe-t-il lorsqu’une application est partagée entre des personnes sur un appareil ?**

L’Adobe contient des informations minimales qui s’associent directement à un utilisateur spécifique. Il associe les données à l’aide d’un UUID créé de manière aléatoire qui est conservé dans les données de l’application et transmis dans chaque requête initiée par l’application. Cela signifie que les utilisateurs finaux partageant l’application sur le même appareil utilisent le même UUID et que toutes les données sont considérées comme détenues par la personne qui effectue la requête RGPD. Pour les demandes d’accès et de suppression, DPSC considère les personnes qui partagent une application comme une seule et même personne.

**Quelles données personnelles sont suivies avec Analytics ?**

Aucune. Des données sont suivies, mais elles se trouvent au niveau de l’application (et non au niveau personnel). Cela inclut les événements tels que les lancements, les blocages, les fermetures, les activités, les achats ou les recouvrements de portfolio. Les emplacements géographiques, les noms, les identifiants d’appareil ou les adresses IP ne sont pas suivis.

**L’utilisateur final a fourni ses informations, mais rien n’a été trouvé. Pourquoi pas ?**

À mesure que le produit Digital Publishing Suite évoluait, les implémentations de service ont été modifiées et davantage de données ont été obscurcies. Si aucune donnée n’a été trouvée à l’aide des données fournies par l’utilisateur, cela signifie que les données de l’utilisateur ne peuvent pas être suivies jusqu’à cette personne.

### Exemple {#example}

Contactez l’assistance clientèle d’Adobe afin de pouvoir lancer une demande RGPD.

Voici un exemple des entrées et des sorties résultantes d’une requête RGPD Digital Publishing Suite :

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
