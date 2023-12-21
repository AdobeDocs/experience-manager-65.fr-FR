---
title: Rendu du modèle de formulaire pour des formulaires HTML5
description: Les profils de HTML5 forms sont associés aux rendus de profil. Les rendus de profil sont des pages JSP chargées de générer la représentation par HTML du formulaire en appelant le service Forms OSGi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 38%

---

# Rendu du modèle de formulaire pour des formulaires HTML5 {#rendering-form-template-for-html-forms}

## Point de terminaison du rendu {#render-endpoint}

Les formulaires HTML5 intègrent la notion de **Profils**, lesquels sont exposés en tant que points d’entrée REST pour activer le rendu sur périphériques mobile des modèles de formulaire. Ces profils sont associés à des **rendus de profil**. Ce sont des pages JSP chargées de générer la représentation HTML du formulaire en appelant le service Forms OSGi. Le chemin d’accès JCR du noeud de profil détermine l’URL du point de fin du rendu. Le point de fin de rendu par défaut du formulaire pointant vers le profil &quot;default&quot; ressemble à ceci :

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

Par exemple, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Pour un profil personnalisé, le point de terminaison change en conséquence. Par exemple, le point de fin du profil personnalisé nommé hrforms est le suivant :

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si votre modèle réside dans le référentiel AEM d’une application appelée FormSubmission, l’URI est :

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Paramètres de rendu {#render-parameters}

Les paramètres de requête pris en charge lors du rendu du formulaire en tant que HTML sont les suivants :

<table>
 <tbody>
  <tr>
   <th><strong>Paramètre </strong></th>
   <th><strong>Description</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Ce paramètre spécifie le nom du fichier de modèle.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Ce paramètre spécifie le chemin d’accès à l’emplacement où se trouvent le modèle et les ressources associées. Ce chemin d’accès peut être le chemin d’accès au système de fichiers du serveur, au référentiel ou au chemin d’accès http ou ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Ce paramètre spécifie l’URL à laquelle le fichier XML de données de formulaire est publié.<br /> </td>
  </tr>
 </tbody>
</table>

### Fusionner les données avec le modèle de formulaire {#merge-data-with-form-template}

| Paramètre | Description |
|---|---|
| dataRef | Ce paramètre indique le **chemin d’accès absolu** du fichier de données fusionné avec le modèle. Ce paramètre peut être une adresse URL d’accès à un service REST renvoyant les données au format XML. |
| data | Ce paramètre spécifie les octets de données codés UTF-8 qui sont fusionnés avec le modèle. Si ce paramètre est spécifié, le formulaire HTML5 ignore le paramètre dataRef . |

### Transmission du paramètre de rendu {#passing-the-render-parameter}

Les formulaires HTML5 prennent en charge trois méthodes pour transmettre les paramètres de rendu. Vous pouvez transférer des paramètres via des URL, des paires clé-valeur et un noeud de profil. Dans le paramètre de rendu, la paire clé-valeur a la priorité la plus élevée, suivie du noeud de profil. Le paramètre de requête d’URL a la priorité la plus faible.

* **paramètres de requête d’URL**: vous pouvez spécifier les paramètres de rendu dans l’URL. Dans les paramètres de requête d’URL, les paramètres sont visibles par l’utilisateur final. Par exemple, l’URL d’envoi suivante contient le paramètre de modèle dans l’URL : `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`.

* **Paramètres de requête SetAttribute**: vous pouvez spécifier les paramètres de rendu en tant que paire clé-valeur. Dans les paramètres de requête SetAttribute, les paramètres ne sont pas visibles par l’utilisateur final. Vous pouvez transférer une requête depuis un autre JSP vers le JSP de rendu de profil HTML5 et utiliser *setAttribute* sur l’objet de la requête pour transmettre tous les paramètres de rendu. Cette méthode a la priorité la plus élevée.

* **Paramètres de demande de nœud de profil :** vous pouvez spécifier les paramètres de rendu en tant que propriétés de nœud d’un nœud de profil. Dans les paramètres de requête du noeud de profil, les paramètres ne sont pas visibles par l’utilisateur final. Le noeud de profil est le noeud où la requête est envoyée. Pour spécifier des paramètres en tant que propriétés de noeud, utilisez CRXDE Lite.

### Paramètres d’envoi {#submit-parameters}

Les formulaires HTML5 envoient des données ; exécutent les scripts et les services Web côté serveur sur des serveurs AEM. Pour plus d’informations sur les paramètres utilisés pour exécuter les scripts et les services côté serveur sur les serveurs AEM, voir [Proxy de service HTML5 Forms](/help/forms/using/service-proxy.md).
