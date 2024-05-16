---
title: Rendu du modèle de formulaire pour des formulaires HTML5
description: Les profils de formulaires HTML5 sont associés aux rendus de profil. Ce sont des pages JSP chargées de générer la représentation HTML du formulaire en appelant le service Forms OSGi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '535'
ht-degree: 100%

---

# Rendu du modèle de formulaire pour des formulaires HTML5 {#rendering-form-template-for-html-forms}

## Point d’entrée de rendu {#render-endpoint}

Les formulaires HTML5 intègrent la notion de **Profils**, lesquels sont exposés en tant que points d’entrée REST pour activer le rendu sur périphériques mobile des modèles de formulaire. Ces profils sont associés à des **rendus de profil**. Ce sont des pages JSP chargées de générer la représentation HTML du formulaire en appelant le service Forms OSGi. Le chemin d’accès JCR du nœud de profil détermine l’URL du point d’entrée du rendu. Le point d’netrée de rendu par défaut du formulaire pointant vers le profil « default » ressemble à :

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

Par exemple, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Pour un profil personnalisé, le point d’entrée change en conséquence. Par exemple, le point d’entrée du profil personnalisé nommé hrforms est le suivant :

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si votre modèle réside dans le référentiel AEM d’une application appelée FormSubmission, l’URI est :

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Paramètres de rendu {#render-parameters}

Les paramètres de requête pris en charge lors du rendu du formulaire au format HTML sont les suivants :

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
   <td>Ce paramètre spécifie le chemin d’accès à l’emplacement où se trouvent le modèle et les ressources associées. Ce chemin d’accès peut être le chemin d’accès au système de fichiers du serveur, au référentiel ou un chemin d’accès http ou ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Ce paramètre spécifie l’URL à laquelle le fichier XML de données de formulaire est publié.<br /> </td>
  </tr>
 </tbody>
</table>

### Fusionner des données avec le modèle de formulaire {#merge-data-with-form-template}

| Paramètre | Description |
|---|---|
| dataRef | Ce paramètre indique le **chemin d’accès absolu** du fichier de données fusionné avec le modèle. Ce paramètre peut être une adresse URL d’accès à un service REST renvoyant les données au format XML. |
| data | Ce paramètre spécifie les octets de données encodés au format UTF-8 qui sont fusionnés avec le modèle. Si ce paramètre est spécifié, le formulaire HTML5 ignore le paramètre dataRef. |

### Passage du paramètre de rendu {#passing-the-render-parameter}

Les formulaires HTML5 prennent en charge trois méthodes pour transmettre les paramètres de rendu. Vous pouvez transférer des paramètres via des URL, des paires clé-valeur et un nœud de profil. Dans le paramètre de rendu, la paire clé-valeur a la priorité la plus élevée, suivie du nœud de profil. Le paramètre de requête d’URL a la priorité la plus faible.

* **Paramètres de requête d’URL** : vous pouvez spécifier les paramètres de rendu dans l’URL. Dans les paramètres de requête d’URL, les paramètres sont visibles par l’utilisateur final ou l’utilisatrice finale. Par exemple, l’URL d’envoi suivante contient le paramètre de modèle dans l’URL : `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`.

* **Paramètres de requête SetAttribute** : vous pouvez spécifier les paramètres de rendu en tant que paire clé-valeur. Dans les paramètres de requête SetAttribute, les paramètres ne sont pas visibles par l’utilisateur final ou l’utilisatrice finale. Vous pouvez transférer une requête depuis un autre JSP vers le JSP de rendu de profil HTML5 et utiliser *setAttribute* sur l’objet de la requête pour transmettre tous les paramètres de rendu. Cette méthode a la priorité la plus élevée.

* **Paramètres de demande de nœud de profil :** vous pouvez spécifier les paramètres de rendu en tant que propriétés de nœud d’un nœud de profil. Dans les paramètres de requête du nœud de profil, les paramètres ne sont pas visibles par l’utilisateur final ou l’utilisatrice finale. Le nœud de profil est le nœud où la requête est envoyée. Pour spécifier des paramètres en tant que propriétés de nœud, utilisez CRXDE Lite.

### Paramètres d’envoi {#submit-parameters}

Les formulaires HTML5 envoient des données ; exécutent les scripts et les services Web côté serveur sur des serveurs AEM. Pour plus d’informations sur les paramètres utilisés pour exécuter les scripts et les services web côté serveur sur les serveurs AEM, voir [Proxy de service des formulaires HTML5](/help/forms/using/service-proxy.md).
