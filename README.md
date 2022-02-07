# ProjetRadar-Camera

On a cropé les images pour obtenir une dimension de 160 par 80, centré sur la route.

On obtient les images radar suivantes : 
<img src="/image/radar_origin.png" width="400">

Ainsi que la segmenetation suivante :
<img src="/image/radar_segmentation.png" width="400">

On instancie le modèle Unet provenant du Kaggle sur la segmentation des nucleis.
On commence par normaliser les données puis on entraine le réseau de neurone sur les images cropées.
Les paramètres d'entrainement sont les suivants :

```
lr_reduction = ReduceLROnPlateau(monitor='val_loss', patience=3, verbose=1, factor=0.5, min_lr=0.000001)
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=[dice_coef, iou_coef])
history = model.fit(X_train,y_train, epochs=40, batch_size=10, validation_data=(X_test,y_test), callbacks=[lr_reduction])
```
