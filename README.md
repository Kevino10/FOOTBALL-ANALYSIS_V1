# football_analysis

🧠 FOOTBALL VIDEO ANALYSIS TOOL – README
Un outil complet de tracking football à partir de vidéo, intégrant IA, interface utilisateur et génération de rapports.
🚀 Objectif général
Permettre à un club ou analyste :
D’analyser un match depuis une simple vidéo
De suivre les déplacements des joueurs et du ballon
De structurer les données dans un XML exploitable
De générer des rapports collectifs ou individuels
De naviguer dans une interface simple et visuelle
🗂 Structure par modules
L’outil est découpé en 6 modules logiques, utilisables via une interface Streamlit.
✅ Module 1 — Initialisation Match
📁 Création automatique de la structure du projet :
input/video.mp4
output/xml_tracking.xml
models/
📄 Permet de centraliser les fichiers du match
📍 Donne le point de départ du pipeline
✅ Module 2 — Calibration Terrain
📷 Détection automatique des keypoints terrain via un modèle YOLOv8 pose
🧮 Calcul de la matrice d’homographie pour projeter les coordonnées en top-down
🔍 Interface de validation visuelle
💾 Sauvegarde : output/tracking_data/homography_matrix.npy
✅ Module 3 — Tracking Joueurs & Ballon
📦 Utilisation d’un modèle IA YOLOv8 pour détecter :
player, goalkeeper, referee, ball
🔁 Tracking frame par frame (avec ou sans DeepSort)
🔢 Projection top-down via homographie
🧾 Génération du fichier output/xml_tracking.xml
(Option) OCR des maillots
✅ Format XML standard :
<frame id="12">
  <object id="5" type="player" team_id="team_1" x_vid="123" y_vid="431" x_proj="41.2" y_proj="28.5" />
</frame>
✅ Module 4 — Assignation Équipes
🎨 Clustering couleur (KMeans) sur les joueurs
🖼 Affichage des miniatures dans Streamlit
🧑 Sélection manuelle du cluster : team 1 / team 2
🛠️ Réaffectation manuelle par player_id
💾 Fichier généré : team_labels.json
{
  "player_6": "team_1",
  "player_21": "team_2"
}
✅ Module 4.5 — Fusion des IDs suspects
🔍 Détection des doublons d’identifiants (ReID, OCR, position…)
🧠 Suggestions de fusions automatiques
🖼 Visualisation des paires dans Streamlit
🧑 Validation manuelle des fusions
📄 Sorties :
fusions.json (journal)
xml_tracking_final.xml (version fusionnée)
✅ Module 5 — Visualisation & Vérification
🎞 Lecture vidéo annotée (bounding boxes, ID, couleurs)
🧭 Carte top-down avec tous les joueurs et le ballon
📋 Liste par frame des objets
🛠 Interface de correction (team_id, suppression objet)
💾 Fichier généré : xml_tracking_final_corrected.xml
🔜 Module 6 — Analyse & Rapport (à venir)
6.1 Analyse collective
📊 Stats d’équipe (distance, vitesse, possession…)
🧠 Heatmaps collectives
📥 Rapport PDF exportable
6.2 Analyse individuelle
👟 Stats joueur par joueur
🔴 Heatmaps individuelles
🗂 Rapport PDF individuel
6.3 Génération de vidéos
📺 Extraits vidéos des actions (passes, tirs, récupérations)
🎞 Extraction automatique avec moviepy ou ffmpeg
🧠 Technologies utilisées
Composant	Outil / Lib
IA détection	YOLOv8 custom
Détection keypoints	YOLOv8 Pose
OCR maillot (option)	easyOCR
Tracking objets	DeepSort (option)
Clustering	KMeans (sklearn)
Interface	Streamlit
Affichage terrain	mplsoccer
Vidéo	OpenCV
Export vidéos (à venir)	MoviePy
✅ À quoi ça sert ?
📊 Gagner du temps sur l’analyse
📈 Mieux visualiser les déplacements
📂 Structurer les données pour les stats
🧑‍💻 Créer des rapports semi-automatiques
🧠 Outil évolutif compatible avec une vision produit
🏁 Prochaines étapes
🔁 Consolider DeepSort pour stabilité des IDs
⚽️ Améliorer le tracking du ballon
🔄 Automatiser les événements (passes, tirs…)
📥 Générer des événements.csv
📊 Finaliser l’analyse (module 6)
# V1_FA
