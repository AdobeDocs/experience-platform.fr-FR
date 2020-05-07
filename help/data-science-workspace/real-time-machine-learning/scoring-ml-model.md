---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Score un modèle d'apprentissage automatique en temps réel
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Score un modèle d&#39;apprentissage automatique en temps réel

>[!IMPORTANT]
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

Ce didacticiel vous explique comment utiliser les noeuds d’apprentissage automatique en temps réel pour prétraiter les données entrantes et les noter par rapport à votre modèle ONNX.

>[!IMPORTANT]
> - Les fonctions utilisées dans les noeuds ne peuvent pas être sérialisées. Par exemple, une fonction lambda utilisée dans un noeud pandas.
> - Le déploiement des arêtes s&#39;effectue manuellement pendant 60 secondes. Il est possible de transférer cette valeur à la méthode score_edge d&#39;EdgeUtils.


>[!NOTE]
>Afin de marquer un modèle pour l&#39;apprentissage automatique en temps réel, vous devez avoir suivi le didacticiel précédent sur la [formation d&#39;un modèle pour l&#39;apprentissage automatique en temps réel.](./training-ml-model.md)

## Créer un bloc-notes

Dans l’interface utilisateur d’Adobe Experience Platform, sélectionnez **[!UICONTROL Ordinateurs portables]** dans *Data Science*. Ensuite, sélectionnez **[!UICONTROL JupyterLab]** et accordez un peu de temps pour que l&#39;environnement se charge.

![ouvrir JupyterLab](../images/rtml/open-jupyterlab.png)

Début en sélectionnant le bloc-notes **Python 3** vide dans le lanceur JupyterLab.

![python blanc](../images/rtml/python-blank.png)

## Importer et découvrir des noeuds

Début en important tous les packages requis pour votre modèle. Assurez-vous que tous les packages que vous prévoyez d’utiliser pour la création de noeuds sont importés.

>[!NOTE]
>La liste des importations peut différer selon le modèle que vous avez élaboré.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Pour voir la liste des noeuds disponibles, copiez et collez l&#39;exemple suivant dans votre bloc-notes.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

La réponse reçue est une liste de noeuds.

![liste des notes](../images/rtml/node-list.png)

## Création de noeuds pour le score d’arête

Ensuite, vous devez définir et créer un noeud pour le score d’arête. Remplacez l’exemple `model_id` par l’ID de modèle que vous avez reçu après avoir suivi une formation dans le didacticiel [](./training-ml-model.md)précédent. Cet exemple utilise le noeud Pandas pour importer une méthode pd.DataDrame ou une fonction générale pandas de niveau supérieur. La fonction de mappage est importée et utilisée pour créer deux noeuds. Pour plus d’informations sur les noeuds disponibles et sur leur utilisation, consultez le guide [de référence des](./node-reference.md)noeuds.

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## Créer une image DSL

Une fois les noeuds créés, l’étape suivante consiste à les relier pour créer un graphique.

Début en répertoriant tous les noeuds qui font partie du graphique.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

Ensuite, connectez les noeuds aux bords. Chaque tuple est une connexion de bord.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Une fois vos noeuds connectés, créez le graphique.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Publier sur le bord

Maintenant que vous avez créé un graphique, vous pouvez le déployer sur le bord.

>[!IMPORTANT]
>Ne publiez pas souvent sur Edge, cela peut surcharger les noeuds Edge. Il n’est pas recommandé de publier le même modèle plusieurs fois.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Client Edge

Une fois la publication effectuée sur le bord, le score est effectué par une requête POST d’un client. En règle générale, cela peut être fait à partir d’une application cliente qui a besoin de scores ML. Vous pouvez aussi le faire depuis Postman. Ici, EdgeUtils est utilisé pour démontrer le processus.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

Une fois que le score est terminé, l’URL du bord, la charge utile et la sortie notée du bord sont renvoyées.

![score terminé](../images/rtml/scoring-complete.png)

## Suppression d’une application déployée à partir d’un bord (facultatif)

>!![CAUTION]
Cette cellule est utilisée pour supprimer votre application Edge déployée. N&#39;utilisez pas la cellule suivante, sauf si vous devez supprimer une application Edge déployée.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Étapes suivantes

En suivant le tutoriel ci-dessus, vous avez réussi à marquer et à déployer votre modèle d’apprentissage automatique en temps réel. Si vous souhaitez en savoir plus sur les noeuds disponibles pour la création de modèles, consultez le guide [de référence des](./node-reference.md)noeuds.



