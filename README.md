# ProjetRadar-Camera

On a cropé les images pour obtenir une dimension de 160 par 80, centré sur la route.

On obtient les images radar suivantes : 

<img src="/image/radar_origin.png" width="800">

Ainsi que la segmenetation suivante :

<img src="/image/radar_segmentation.png" width="800">

On instancie le modèle Unet provenant du Kaggle sur la segmentation des nucleis.
On commence par normaliser les données puis on entraine le réseau de neurone sur les images cropées.
Les paramètres d'entrainement sont les suivants :

```
lr_reduction = ReduceLROnPlateau(monitor='val_loss', patience=3, verbose=1, factor=0.5, min_lr=0.000001)
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=[dice_coef, iou_coef])
history = model.fit(X_train,y_train, epochs=40, batch_size=10, validation_data=(X_test,y_test), callbacks=[lr_reduction])
```

Pour mesurer la performance on utilise le dice_coef et iou_coef. Sur les données tests (10% de la dataset), on obtient les performances suivantes :
```
dice_coef = 71,36% 
Iou_coef: 62,06%
```

On enregistre le fichier de modèle et les poids (folder model_weight).

Pour finir, on prédit quelques images radar à partir du modèle. On obtient les résultats suivants :

Segmentation prédite à partir d'image radar :

<img src="/image/radar_predict.png" width="800">

La vraie segmenetation (ground truth) :

<img src="/image/radar_groundtruth.png" width="800">



Pour les images 272x80 :


```
dice_coef = 66,21% 
Iou_coef: 53,70%
```
