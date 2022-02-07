# ProjetRadar-Camera

On a cropé les images pour obtenir une dimension de 160 par 80, centré sur la route.

On obtient les images radar suivantes : 
<img src="/image/radar_origin" width="400">

Ainsi que la segmenetation suivante :
<img src="/image/radar_segmentation" width="400">

On instancie le modèle Unet provenant du Kaggle sur la segmentation des nucleis.
On commence par normaliser les données puis on entraine le réseau de neurone sur les images cropées.
Les paramètres d'entrainement sont les suivants :



