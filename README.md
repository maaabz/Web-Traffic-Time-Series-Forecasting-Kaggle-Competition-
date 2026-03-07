Web Traffic Time Series Forecasting
=====================================

J'ai participé à la compétition Kaggle suivante pour m'entraîner sur les séries temporelles (la compétition a 9 ans quand j'écris ce readme) :
https://www.kaggle.com/competitions/web-traffic-time-series-forecasting

L'objectif était d'explorer plusieurs approches différentes par curiosité et apprentissage.


1. XGBoost
   On m'avait conseillé ce modèle, réputé comme l'un des plus performants. J'ai obtenu un bon
   résultat sur un échantillon de données, bien que je n'aie pas soumis les prédictions sur
   la compétition Kaggle.

2. Réseau de neurones
   J'ai ensuite décidé d'implémenter une solution basée sur un réseau de neurones.
   Deux fichiers correspondent à cette approche :

   - Fichier "_w"  : Version fonctionnelle ayant obtenu un score de 43.84017 sur la compétition.
   - Fichier "_dk" : Tentative d'amélioration de la version précédente, qui ne fonctionne malheureusement pas en raison d'un problème de dimensions des tableaux. Lors du développement du réseau de neurones, j'ai été confronté à un problème de mémoire RAM : le code consommait plus de mémoire que ce que Kaggle autorise, ce qui générait une erreur d'exécution. J'ai tenté de réduire l'empreinte mémoire, mais sans succès.
