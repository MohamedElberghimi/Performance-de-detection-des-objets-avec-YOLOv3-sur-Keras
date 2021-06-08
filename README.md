# Performance-de-detection-des-objets-avec-YOLOv3-sur-Keras

Le fonctionnement de YOLO peut être présenté par les étapes suivantes :
1-	YOLO prend une image en entrée.
2-	L’image est découpée en N*N cellules.
3-	A chaque cellule, on associe un vecteur de (5+C) *B éléments. Ces éléments sont :
-Pc : exprime la probabilité qu’un objet est présent dans la cellule.
-bx, by, bh, bw; sont des coordonnées pour spécifier un boundig box (un rectangle qu’on trace autour de l’objet détecté) lorsque un objet est présent dans la cellule.
-C éléments : correspondent aux probabilités qu’un objet détecté appartient à chacune des C classes.
-B : représente le nombre de bounding boxes qu’on peut avoir par cellule. On les appelle Anchor Boxes.

4-	Eliminer les bounding boxes avec une probabilité Pc inférieure à un certain seuil.
5-	Appliquer la méthode Non-Max suppression pour éliminer les bounding boxes détectant le même objet. Le Non-Max suppression se fait en deux étapes :
		  Etape1 : On choisit le bounding box avec la probabilité Pc la plus                                           
      Etape2 : supprimer tout bounding box avec un IoU avec le box choisi dans l’étape1 supérieur à un certain seuil.


  Evaluer une prédiction :
Pour juger une prédiction de bonne ou mauvaise, on s’appuie sur le rapport IoU entre le bounding box prédit et le vrai bounding box. Si le IoU est supérieur à un certain seuil, la prédiction est bonne, Sinon la prédiction est mauvaise. 
  
  Phase d’entrainement :
L’entrainement du modèle se fait avec comme entrée nos images aves les labels y associés de dimension N*N*(number of anchor boxes) *(5+number of classes), avec N*N est le nombre de cellules.

  Phase de test :
La phase de test consiste à prédire la sortie d’une image jamais vue par le modèle. On découpe l’image en cellules de la même manière que les images d’entraînement. Après, on fait passer l’image à travers un réseau de neurones convolutif qui retourne une sortie de dimension (N,N,number of anchor boxes, ,5,number of classes), on applique un flattening aux deux dernières dimensions, ce qui donne une sortie de dimension (N,N,number of anchor boxes, ,5*number of classes), enfin on applique la technique de Non-Max suppression pour éviter de sélectionner des boxes qui se chevauchent. 

  Experiencor YOLO3 pour Keras Project :
Implémenter un modèle from scratch est difficile, surtout pour les débutants, c’est pourquoi on va faire appel à une implémentation tiers pour avoir des modèles déjà implémentés et pré-entraînés. Dans ce projet, on utilisera un des projets les plus utilisés pour travailler avec des modèles YOLO pré-entrainés, il s’agit de “keras-yolo3 : Training and Detecting Objects with YOLO3” ou experiencor.
