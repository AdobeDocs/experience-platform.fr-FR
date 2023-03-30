---
title: Messages d’erreur relatifs aux sources
description: Découvrez les messages d’erreur que vous pouvez rencontrer lors de l’utilisation du service de flux pour les sources.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 9%

---

# Messages d’erreur relatifs aux sources

Ce document fournit un catalogue de messages d’erreur, des descriptions et des suggestions de résolutions pour les sources.

## Erreurs génériques

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1000-400` | Mauvaise requête | La requête n’est pas valide. Vérifiez la demande et réessayez. |
| `1001-401` | Non autorisé | L’utilisateur n’est pas autorisé. Contactez votre administrateur pour accéder à la ressource. |
| `1002-403` | Interdit | L’opération demandée est interdite. Vérifiez l’opération demandée et réessayez. |
| `1003-404` | Ressource introuvable | La ressource demandée est introuvable. Vérifiez la requête fournie et réessayez. |
| `1004-415` | Type de média non pris en charge | Le format de payload fourni n’est pas pris en charge. Vérifiez votre requête fournie et réessayez. |
| `1005-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1006-408` | Délai d’expiration de la requête | Une erreur s’est produite lors du traitement de la requête. La demande a été expirée. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1007-400` | Paramètre d’en-tête non valide | Un paramètre d’en-tête non valide : {headerName} a été reçu. Vérifiez les paramètres d’en-tête et réessayez. |
| `1008-401` |  | Jeton d’autorisation non valide | Le jeton d’autorisation n’a pas accès à cette organisation ou l’organisation n’existe pas. Assurez-vous que l’organisation existe ou contactez votre administrateur pour y accéder. |
| `1009-403` | ID d’organisation IMS manquant ou vide | L’en-tête de la demande d’ID d’organisation est manquant ou vide. Mettez à jour la valeur de l’en-tête et réessayez. |
| `1010-500` | Message détaillé non valide | Le paramètre du message détaillé n’a pas été correctement fourni. Vérifiez le paramètre dans le message détaillé et réessayez. |
| `1011-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1012-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1013-412` | Echec de la condition | La condition définie par les en-têtes If-Unmodified-Since ou If-None-Match n’est pas remplie. Veuillez vérifier et réessayer. |
| `1014-400` | Argument illégal de requête incorrect | La requête n’a pas pu être traitée. {detailMessage} |

## Erreurs de structure

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1100-400` | Requête incorrecte | La requête n’a pas pu être traitée. {detailMessage} |
| `1101-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1102-404` | Ressource introuvable | La ressource demandée est introuvable. {detailMessage} |
| `1103-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1104-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1105-401` | Non autorisé | L’utilisateur n’est pas autorisé. {detailMessage} |
| `1106-403` | Interdit | L’opération demandée est interdite. {detailMessage} |
| `1107-412` | Echec de la condition | La condition définie par les en-têtes If-Unmodified-Since ou If-None-Match n’est pas remplie. {detailMessage} |

## Erreurs de chiffrement

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1200-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1201-400` | Requête incorrecte | flowId ne peut pas être nul ou vide. Veuillez fournir un flowId valide dans la demande et réessayer. |
| `1202-400` | Requête incorrecte | PublicKeyId est absent dans les transformations={transformations} du flux. Indiquez publicKeyId dans la requête et réessayez. |
| `1203-400` | Requête incorrecte | La clé de chiffrement n’existe pas par rapport à keyID={keyID} dans les transformations={transformations} du flux. Vérifiez votre ID de clé fourni et réessayez. |
| `1204-400` | Requête incorrecte | L’algorithme de chiffrement fourni n’est pas valide. Veuillez fournir un algorithme de chiffrement valide et réessayer. |
| `1205-400` | Requête incorrecte | La phrase secrète est absente de la section params de la requête fournie. Veuillez fournir passExpression dans les paramètres et réessayer. |

## Erreurs de l’API REST

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1300-400` | Requête incorrecte | La demande de connexion de correctif n’est pas prise en charge pour le connecteur {connectorType}. Vérifiez la requête fournie et réessayez. |
| `1301-400` | Requête incorrecte | Param authSpecType fourni : {authSpecType} n’est pas pris en charge. Indiquez un type de spécification d’authentification valide et réessayez. |
| `1302-400` | Requête incorrecte | Le type d’authentification fourni = {authType} n’est pas pris en charge pour connector={connectorType}. Veuillez fournir un type d’authentification valide pour le connecteur donné. |
| `1303-400` | Requête incorrecte | L’URL n’a pas pu être codée avec les paramètres d’authentification donnés, car le codage d’URL n’est pas pris en charge pour {value}. Vérifiez vos paramètres d’authentification et réessayez. |
| `1304-400` | Requête incorrecte | Le champ obligatoire {field} n’est pas fourni. Veuillez fournir le {champ} et réessayer. |
| `1305-400` | Requête incorrecte | Le type de connecteur fourni = {connectorType} n’est pas pris en charge pour cette opération. |
| `1306-400` | Requête incorrecte | La connexion cible ne peut pas être nulle lors de la validation de l’identifiant de spécification de connexion cible. Vérifiez la requête fournie et réessayez. |
| `1307-400` | Requête incorrecte | L’identifiant de spécification de connexion cible n’est pas valide={targetConnectionSpecId}. La valeur autorisée est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Requête incorrecte | La requête n’a pas pu être traitée. Message d’erreur : {msftErrorMessage} |
| `1309-400` | Requête incorrecte | La transformation de chiffrement fournie n’est pas valide car {requiredParam} est absent des paramètres. Veuillez fournir {requiredParam} et réessayer. |
| `1310-400` | Requête incorrecte | Le publicKeyId fourni dans les paramètres a expiré. Veuillez fournir un publicKeyId valide et réessayer. |
| `1311-400` | Requête incorrecte | Le publicKeyId fourni dans params n’est pas valide. Veuillez fournir un publicKeyId valide et réessayer. |
| 1312-400 | Requête incorrecte | La valeur de paramètre fournie {paramValue} n’est pas une entrée valide pour property={requestParam}. Indiquez une valeur de paramètre valide et réessayez. |
| `1313-400` | Requête incorrecte | L’attribut de chemin {attribute} n’existe pas. Vérifiez que l’attribut existe et réessayez. |
| `1314-400` | Requête incorrecte | Un chemin complexe a été fourni, mais n’est pas autorisé. Vérifiez que le chemin complexe n’est pas fourni et réessayez. |
| `1315-400` | Requête incorrecte | Le chemin d’accès fourni {path} doit pointer vers un tableau d’enregistrements. Assurez-vous que le chemin d’accès fourni pointe vers le tableau d’enregistrements et réessayez. |
| `1316-400` | Requête incorrecte | Les paramètres de pagination fournis ne doivent pas être vides. Indiquez des paramètres de pagination valides et réessayez. |
| `1317-400` | Requête incorrecte | Les paramètres de planification fournis sont vides, mais ne doivent pas être vides. Indiquez des paramètres de planification valides et réessayez. |
| `1318-400` | Requête incorrecte | {combinaisonMessage}. Vérifiez la requête fournie et réessayez. |
| `1319-400` | Requête incorrecte | {param} doit faire partie de la collection parent. Veuillez fournir {param} dans la collection parente et réessayer. |
| `1320-400` | Requête incorrecte | {idType} ne peut pas être nul ou vide. Veuillez fournir un {idType} valide et réessayer. |
| `1321-400` | Requête incorrecte | La longueur de {idType} doit être un, la taille fournie est {size}. Indiquez une taille valide et réessayez. |
| `1322-400` | Requête incorrecte | La connexion source ne peut pas être nulle pour la création de la référence de schéma. Indiquez une connexion source valide et réessayez. |
| `1323-400` | Requête incorrecte | L’entité {entity} ne peut pas être nulle ou vide dans la connexion source : {sourceConnection}. Veuillez fournir un {entity} valide et réessayer. |
| `1324-400` | Requête incorrecte | La connexion cible ne peut pas être nulle lors de l’extraction de l’identifiant du jeu de données. Indiquez une connexion cible valide et réessayez. |
| `1325-400` | Requête incorrecte | Le paramètre dataSetId ne peut pas être nul ou vide dans la connexion cible : {TargetConnection}. Indiquez un paramètre dataSetId valide et réessayez. |
| `1326-400` | Requête incorrecte | La connexion source ne peut pas être nulle lors de la récupération du format source. Indiquez une connexion source valide et réessayez. |
| `1327-400` | Requête incorrecte | Le format des données source fournies={sourceFormat} dans SourceConnection n’est pas pris en charge. Les valeurs autorisées sont les suivantes : {values}. Indiquez les valeurs autorisées et réessayez. |
| `1328-400` | Requête incorrecte | La transformation de mappage ne peut pas être nulle lors de l’extraction de {param}. Veuillez fournir une transformation de mappage valide et réessayer. |
| `1329-400` | Requête incorrecte | Le paramètre : {param} ne peut pas être nul ou vide dans la requête fournie. Veuillez fournir un {param} valide et réessayer. |
| `1330-400` | Requête incorrecte | Aucune colonne n’a été trouvée pour table {tableName}. Indiquez un nom de table valide et réessayez. |
| `1331-400` | Requête incorrecte | Le délimiteur de colonne ne peut pas contenir plus d’un caractère dans SourceConnection : {sourceConnection}. Indiquez un délimiteur de colonne valide, puis réessayez. |
| `1332-400` | Requête incorrecte | La demande de connexion source avec connectionSpecId : {connectionSpecId} ne peut pas avoir de baseConnectionId. Supprimez le baseConnectionId et réessayez. |
| `1333-400` | Requête incorrecte | flowRunAction={flowRunAction} n’est pas pris en charge pour la source avec la spécification id={specId}. Fournissez une action d’exécution de flux valide et réessayez. |
| `1334-400` | Requête incorrecte | Le paramètre de requête : {param} ne peut pas être vide. Veuillez fournir un {param} valide et réessayer. |
| `1335-400` | Requête incorrecte | Une erreur s’est produite lors de la sérialisation des paramètres de filtre à explorer. Vérifiez votre requête de paramètre de filtre, puis réessayez. |
| `1336-400` | Requête incorrecte | Explorer la connexion n’est pas pris en charge pour l’identifiant de spécification de connexion : {connectionSpecId}. Indiquez l’identifiant de spécification de connexion pris en charge et réessayez. |
| `1337-400` | Requête incorrecte | {QueryParam} ne peut pas être vide pour objectType={objectType}. Veuillez fournir un {QueryParam} valide et réessayer. |
| `1338-400` | Requête incorrecte | L’ID de connexion {connectionType} ne peut pas être nul dans flowRequest. Indiquez un ID de connexion {connectionType} valide dans flowRequest. |
| `1339-400` | Requête incorrecte | Le format de l’organisation={imsOrg} fourni dans la requête n’est pas valide. Indiquez un ID d’organisation valide et réessayez. |
| `1340-400` | Requête incorrecte | Une erreur s’est produite lors de l’analyse de {time}. Vérifiez le format d’heure indiqué dans la requête et réessayez. |
| `1341-400` | Requête incorrecte | Le code Json ODI fourni est vide. Veuillez fournir un code Json ODI valide et réessayer. |
| `1342-400` | Requête incorrecte | Les définitions du segment &quot;dls:folder&quot; dans &quot;odi.json&quot; sont manquantes. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1343-400` | Requête incorrecte | Les segments &quot;dls:entityReferences&quot; et &quot;dls:partitionSpec&quot; dans &quot;odi.json&quot; sont des définitions manquantes. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1344-400` | Requête incorrecte | La définition de &quot;dls:partitionSpec&quot; dans &quot;odi.json&quot; n’est pas valide car plusieurs partitionSpecs ont été trouvés. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1345-400` | Requête incorrecte | Il manque des définitions dans 1 ou plusieurs segments dans les chemins : &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; dans &#39;odi.json&#39;. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1346-400` | Requête incorrecte | La définition &quot;@type&quot; fournie dans &quot;dls:fileFormat&quot; dans &quot;odi.json&quot; n’est pas valide. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1347-400` | Requête incorrecte | La définition dls:csvDelimiters dans &quot;odi.json&quot; n’est pas prise en charge. Les csvDelimiters pris en charge sont les suivants : [&#39;,&#39;]. Indiquez les définitions appropriées dans &quot;odi.json&quot;, puis réessayez. |
| `1348-400` | Requête incorrecte | Une erreur s’est produite lors de la désérialisation de &quot;dls:entityReferences&quot;. Vérifiez si les données sont dans un format valide et réessayez. |
| `1349-400` | Requête incorrecte | Les paramètres de filtre fournis ne sont pas valides. Indiquez des paramètres de filtre valides et réessayez. |
| `1350-400` | Requête incorrecte | Aucun opérateur n’a été fourni pour le filtre à la source. Indiquez une requête de filtre valide avec l’opérateur approprié, puis réessayez. |
| `1351-400` | Requête incorrecte | L’opérateur fourni {operator} n’est pas pris en charge pour le filtre à la source pour ce connecteur. Indiquez un opérateur valide et réessayez. |
| `1352-400` | Requête incorrecte | L’opérateur fourni {operator} ne peut pas être mappé à un opérateur natif pris en charge pour {ql}. Indiquez un opérateur valide et réessayez. |
| `1353-400` | Requête incorrecte | Le filtre à la source n’est pas encore pris en charge pour le connecteur {connectorType}. Consultez les connecteurs pris en charge dans la documentation : https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Requête incorrecte | Le langage de requête {ql} n’est pas encore pris en charge pour le filtre à la source. Indiquez un langage de requête valide et réessayez. |
| `1355-400` | Requête incorrecte | Le type de filtre fourni n’est pas valide. Le type de filtre pris en charge est le suivant : PQL. Indiquez un type de filtre valide et réessayez. |
| `1356-400` | Requête incorrecte | Le format de filtre fourni n’est pas valide. Le format de filtre pris en charge est le suivant : pql/json. Veuillez fournir un format de filtre valide et réessayer. |
| `1357-400` | Requête incorrecte | Le filtre fourni n’est pas valide. La valeur doit être fournie avec des filtres détaillés. Indiquez un filtre valide et réessayez. |
| `1358-400` | Requête incorrecte | Le paramètre fourni &#39;objectType&#39; n’est pas valide. Veuillez fournir un objectType valide et réessayer. |
| `1359-400` | Requête incorrecte | Le paramètre {param} est manquant dans la requête. Veuillez fournir un {param} valide et réessayer. |
| `1360-400` | Requête incorrecte | L’heure de début ne peut pas être définie dans le passé. Indiquez une heure de début valide et réessayez. |
| `1361-400` | Requête incorrecte | L’intervalle n’est pas autorisé avec l’ingestion d’une seule fois. Supprimez l’intervalle ou modifiez la fréquence, puis réessayez. |
| `1362-400` | Requête incorrecte | L’intervalle ne peut pas être inférieur à {minInterval}. Indiquez une valeur d’intervalle valide et réessayez. |
| `1363-400` | Requête incorrecte | L’intervalle {interval} n’est pas autorisé avec la fréquence : {frequency}. Indiquez une valeur d’intervalle valide et réessayez. |
| `1364-400` | Requête incorrecte | L’indicateur de renvoi n’est pas autorisé lorsque la fréquence est définie sur 1. Supprimez l’indicateur de renvoi lorsque la fréquence est définie sur une fois, puis réessayez. |
| `1365-400` | Requête incorrecte | Le chemin {path} fourni dans ops n’est pas valide. Indiquez un chemin d’accès {path} valide et réessayez. |
| `1366-400` | Requête incorrecte | L’heure de début est passée et l’opération de mise à jour n’est plus autorisée. |
| `1367-400` | Requête incorrecte | La colonne delta est requise dans la transformation de copie lors de la création d’un connecteur CRM. Indiquez la colonne delta et réessayez. |
| `1368-400` | Requête incorrecte | Le mode n’est pas autorisé dans la requête de flux. Vérifiez votre demande, puis réessayez. |
| `1369-400` | Requête incorrecte | La colonne delta dans la transformation de copie n’est pas autorisée lorsque la fréquence est définie sur une seule fois. Supprimez la colonne delta et réessayez. |
| `1370-400` | Requête incorrecte | Les colonnes source n’ont pas pu être récupérées pour l’ingestion, car la transformation de mappage est manquante. Ajoutez la transformation de mapping et réessayez. |
| `1371-400` | Requête incorrecte | La détection des propriétés de fichier n’est pas prise en charge pour le connecteur {connectorType}. Indiquez les propriétés du fichier manuellement. |
| `1372-400` | Requête incorrecte | L’opération actuelle n’est pas autorisée. Explorer via la spécification de connexion n’est pas autorisé pour la spécification de connexion ID={connectionSpecId}. |
| `1373-400` | Requête incorrecte | flowSpecType est absent de la requête. Fournissez un flowSpecType valide et réessayez. |
| `1374-400` | Requête incorrecte | Les paramètres de requête fournis ne sont pas valides. Vous ne pouvez pas avoir l’indicateur de déterminationProperties et les propriétés définies par l’utilisateur dans la même requête. Corrigez votre requête, puis réessayez. |
| `1375-400` | Requête incorrecte | La détection des propriétés du fichier a échoué. Veuillez saisir les propriétés manuellement. |
| `1376-400` | Requête incorrecte | La détection des propriétés du fichier n’est pas prise en charge pour la spécification de connexion id={connectionSpecId}. Indiquez les propriétés du fichier manuellement. |
| `1377-400` | Requête incorrecte | Le paramètre de valeur fourni est nul et ne peut pas être comparé à l’opérateur {operator}. Indiquez un paramètre de valeur valide et réessayez. |
| `1378-400` | Requête incorrecte | Une erreur s’est produite lors de la validation de la colonne d’entrée {column} pour le filtre à la source. Le nom de la colonne doit être une colonne valide dans le tableau. Indiquez un nom de colonne valide et réessayez. |
| `1379-400` | Requête incorrecte | Une erreur s’est produite lors de la validation de l’entrée {value} pour le filtre à la source. La colonne DataType à la source est {columnDataType} et la valeur DataType [Chaîne] ne correspond pas à . Indiquez une valeur {value} valide et réessayez. |
| `1380-400` | Requête incorrecte | Échec de la création de l’exécution du flux. Message d’erreur : {message} |
| `1381-400` | Requête incorrecte | WindowEndTime={endTime} ne peut pas être antérieur à Window StartTime={startTime}. Indiquez une heure de fin valide et réessayez. |
| `1382-400` | Requête incorrecte | La colonne delta doit correspondre à la valeur présente dans les transformations Copy du flux. Indiquez une colonne delta valide et réessayez. |
| `1383-400` | Requête incorrecte | La colonne delta est manquante dans les paramètres reçus pour la création d’une exécution de flux. Indiquez la colonne delta dans les paramètres et réessayez. |
| `1384-400` | Requête incorrecte | Les paramètres={params} fournis pour la création de l’exécution de flux ne sont pas valides ou sont vides. Indiquez des paramètres valides et réessayez. |
| `1385-400` | Requête incorrecte | Le connectorType={connectorType} fourni n’est pas pris en charge pour la création d’exécutions de flux. Fournissez un connectorType valide et réessayez. |
| `1386-400` | Requête incorrecte | flowId={flowId} avec scheduleParams frequency={frequency} n’est pas pris en charge pour la création d’exécutions de flux. Indiquez une fréquence valide et réessayez. |
| `1387-400` | Requête incorrecte | flowRunId={flowRunId} est dans un état non valide={state} pour le redéclenchement. Veuillez réessayer après un certain temps et contactez le service clientèle si le problème persiste. |
| `1388-400` | Requête incorrecte | Le flux={flow} se trouve dans state={state} et ne peut pas être redéclenché. Le flux doit être à l’état activé pour le redéclenchement. |
| `1389-400` | Requête incorrecte | Une erreur s’est produite lors de l’analyse de la chaîne codée en base64 fournie. Indiquez une chaîne de filtre codée valide, puis réessayez. |
| `1390-400` | Requête incorrecte | L’opérateur &quot;not&quot; ne peut pas avoir plusieurs comparaisons. Veuillez fournir un nombre valide de comparaisons et réessayer. |
| `1391-400` | Requête incorrecte | Échec de l’analyse de SchemaMetaData dans sourceConnection pour Id={sourceConnectionId}. Vérifiez le schemaMetaData dans votre requête, puis réessayez. |
| `1392-400` | Requête incorrecte | Échec de l’analyse des transformations dans la requête de flux pour flowId={flowId}. Vérifiez les transformations de votre requête et réessayez. |
| `1393-400` | Requête incorrecte | Le paramètre fourni {parameter} est nul ou vide. Veuillez fournir un {paramètre} valide et réessayer. |
| `1394-400` | Requête incorrecte | La valeur minimale d’un paramètre {parameter} est de un. Veuillez fournir un {paramètre} valide et réessayer. |
| `1395-400` | Requête incorrecte | La connexion source trouvée dans le flux est nulle ou vide. Indiquez une connexion source valide dans le flux et réessayez. |
| `1396-400` | Requête incorrecte | Impossible de trouver un format correspondant. Veuillez fournir un format correspondant et réessayer. |
| `1397-400` | Requête incorrecte | La fréquence fournie : {frequency} n’est pas valide. Indiquez une fréquence valide et réessayez. |
| `1398-400` | Requête incorrecte | L’opération fournie : {action} n’est pas pris en charge. Vérifiez l’opération fournie et réessayez. |
| `1399-400` | Requête incorrecte | Un requestFileType valide est introuvable. Veuillez fournir un requestFileType valide et réessayer. |
| `1400-400` | Requête incorrecte | Le paramètre fourni &quot;templateType&quot; n’est pas valide. Indiquez un type de modèle valide et réessayez. |
| `1401-400` | Requête incorrecte | L’action d’exécution de flux fournie={flowRunAction} n’est pas prise en charge. Indiquez une action d’exécution de flux valide et réessayez. |
| `1402-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1403-400` | Requête incorrecte | L’heure de début est dépassée et vous ne pouvez plus changer la fréquence en une seule fois. |
| `1404-400` | Requête incorrecte | L’heure de début est dépassée et vous ne pouvez plus mettre à jour le renvoi. |

## Exceptions de service de flux (1600-1699)

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1600-400` | Requête incorrecte | La requête n’a pas pu être traitée. {detailMessage} |
| `1601-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1602-404` | Ressource introuvable | La ressource demandée est introuvable. {detailMessage} |
| `1603-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer. Contactez l’assistance clientèle si le problème persiste. |
| `1604-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer. Contactez l’assistance clientèle si le problème persiste. |
| `1605-401` | Non autorisé | L’utilisateur n’est pas autorisé. {detailMessage} |
| `1606-403` | Interdit | L’opération demandée est interdite. {detailMessage} |
| `1607-412` | Echec de la condition | La condition définie par les en-têtes If-Unmodified-Since ou If-None-Match n’est pas remplie. {detailMessage} |

## Erreurs des zones d’entrée de données

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1700-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1701-400` | Requête incorrecte | La zone d’entrée fournie est inactive. Veuillez activer la zone d&#39;entrée et réessayer. |
| `1702-400` | Requête incorrecte | Le type SAS={sasType} fourni pour la zone d’entrée n’est pas autorisé. Veuillez fournir un SAS valide et réessayer. |
| `1703-400` | Requête incorrecte | L’actualisation des informations d’identification n’est pas autorisée. |
| `1704-400` | Requête incorrecte | Les clés renvoyées pour storageAccountName={accountName} dans subscriptionId={subscriptionId} et resourceGroupName={resourceGroupName} sont incorrectes. Vérifiez votre demande, puis réessayez. Veuillez contacter le support si le problème persiste. |
| `1705-400` | Requête incorrecte | L’action de zone d’entrée de données fournie n’est pas prise en charge. Veuillez fournir une action valide et réessayer. |
| `1706-400` | Requête incorrecte | La configuration des activations autorisées n’est pas configurée correctement pour la zone d’entrée={landingZoneType}. Veuillez réessayer et contacter le service clientèle si le problème persiste. |
| `1707-400` | Requête incorrecte | Le service n’a pas pu démarrer, car la configuration de la zone d’entrée ne peut pas être nulle ou vide. Assurez-vous que la configuration de la zone d&#39;entrée n&#39;est pas nulle et réessayez. |
| `1708-400` | Requête incorrecte | La configuration du conteneur ne peut pas être nulle dans landingZoneType={landingZoneType}. Assurez-vous que la configuration du conteneur n’est pas nulle et réessayez. |
| `1709-400` | Requête incorrecte | Les détails du SAS ne peuvent pas être nuls pour {tokenConfig} dans landingZoneType={landingZoneType}. Indiquez un SAS valide dans la configuration et réessayez. |
| `1710-400` | Requête incorrecte | La zone d&#39;entrée de type fournie : {landingZoneUseCase} n’est pas pris en charge. Indiquez un type de zone d’entrée valide et réessayez. |
| `1711-400` | Requête incorrecte | Les détails du SAS sont introuvables pour la zone d’entrée de données fournie de type : {landingZoneUseCase}. Vérifiez si les détails du SAS sont fournis pour le type de zone d’entrée fourni. |
| `1712-400` | Requête incorrecte | L&#39;action de zone d&#39;entrée fournie : {actionType} n’est pas autorisé. Indiquez une action de zone d’entrée de données valide et réessayez. |
| `1713-400` | Requête incorrecte | {OperationType} n’est pas autorisé pour le {tokenType} fourni. Vérifiez votre demande, puis réessayez. |
| `1714-400` | Requête incorrecte | Le clientId={clientId} n’est pas autorisé à effectuer cette opération. Vérifiez votre demande avec des autorisations et réessayez. |