---
keywords: Experience Platform;guide de développement;Espace de travail de science des données;rubriques populaires;machine learning en temps réel;référence de nœud;
solution: Experience Platform
title: Référence des nœuds de machine learning en temps réel
description: Un nœud est l’unité fondamentale à partir de laquelle des graphiques sont formés. Chaque nœud effectue une tâche spécifique et ces nœuds peuvent être liés ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un nœud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence de machine learning. Le nœud sort la valeur transformée ou déduite pour le ou les nœuds suivants.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 100%

---

# Référence des nœuds de machine learning en temps réel (Alpha)

>[!IMPORTANT]
>
>Le machine learning en temps réel n’est pas encore disponible pour tous les utilisateurs et utilisatrices. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document est sujet à modification.

Un nœud est l’unité fondamentale à partir de laquelle des graphiques sont formés. Chaque nœud effectue une tâche spécifique et ces nœuds peuvent être liés ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un nœud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence de machine learning. Le nœud sort la valeur transformée ou déduite pour le ou les nœuds suivants.

Le guide suivant décrit les bibliothèques de nœuds prises en charge pour le machine learning en temps réel.

## Découvrir les nœuds à utiliser dans votre pipeline ML

Copiez le code suivant dans un notebook [!DNL Python] pour afficher tous les nœuds disponibles.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Exemple de réponse**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Nœuds standard

Les nœuds standard s’appuient sur les bibliothèques de science de données open source telles que Pandas et ScikitLearn.

### ModelUpload

Le nœud ModelUpload est un nœud Adobe interne qui prend un model_path et charge le modèle depuis le chemin du modèle local vers le magasin d‘objets blob de machine learning en temps réel.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode est un nœud Adobe interne qui prend un identifiant de modèle pour extraire le modèle ONNX pré-entraîné et l’utilise pour noter les données entrantes.

>[!TIP]
>
>Indiquez les colonnes dans l’ordre selon lequel vous souhaitez que les données soient envoyées au modèle ONNX pour qu’une note soit attribuée.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Le nœud Pandas suivant vous permet d’importer n’importe quelle méthode `pd.DataFrame` ou n’importe quelle fonction générale de niveau supérieur Pandas. Pour en savoir plus sur les méthodes Pandas, consultez la [documentation sur les méthodes Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Pour plus d’informations sur les fonctions de niveau supérieur, consultez le [guide de référence de l’API Pandas pour les fonctions générales](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Le nœud ci-dessous utilise `"import": "map"` pour importer le nom de la méthode sous la forme d’une chaîne dans les paramètres, puis saisit les paramètres sous la forme d’une fonction map. L’exemple ci-dessous effectue cette opération en utilisant `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Une fois le mappage en place, vous avez la possibilité de définir `inplace` comme `True` ou `False`. Définissez `inplace` comme `True` ou `False` selon que vous souhaitez appliquer ou non une transformation sur place. Par défaut `"inplace": False` crée une colonne. La prise en charge d’un nouveau nom de colonne doit être ajoutée dans une version ultérieure. La dernière ligne `cols` peut être un nom de colonne unique ou une liste de colonnes. Indiquez les colonnes sur lesquelles vous souhaitez appliquer la transformation. Dans cet exemple, `device` est spécifié.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

Le nœud ScikitLearn vous permet d’importer n’importe quel modèle ou scaler ScikitLearn ML. Pour plus d’informations sur les valeurs utilisées dans l’exemple, consultez le tableau ci-dessous :

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valeur | Description |
| --- | --- |
| fonctionnalités | Fonctionnalités d’entrée du modèle (liste des chaînes). <br> Par exemple : `browser`, `device`, `login_page`, `product_page`, `search_page` |
| libellé | Nom de la colonne cible (chaîne). |
| mode | Entraînement/test (chaîne). |
| model_path | Chemin d’accès à l’enregistrement local du modèle au format onnx. |
| params.model | Chemin d’accès absolu d’importation au modèle (chaîne de caractères), par exemple : `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Hyperparamètres du modèle, consulter la documentation [API sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) pour plus d’informations. |
| node_instance.process(data_message_from_previous_node) | La méthode `process()` prend DataMsg à partir du nœud précédent et applique la transformation. Cela dépend du nœud actuellement utilisé. |

### Fractionner

Utilisez le nœud suivant pour partager votre Dataframe en entraînement et test en transmettant `train_size` ou `test_size`. Cette opération renvoie un Dataframe avec un multi-index. Vous pouvez accéder aux dataframes d’entraînement et de test à l’aide de l’exemple suivant, `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Étapes suivantes

L’étape suivante consiste à créer des nœuds à utiliser dans la notation d’un modèle de machine learning en temps réel. Pour plus d’informations, consultez le [Guide d’utilisation du notebook de machine learning en temps réel](./rtml-authoring-notebook.md).
