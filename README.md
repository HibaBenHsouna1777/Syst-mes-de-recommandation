# Syst-mes-de-recommandation
Systeme de recommandation des encadrants
Ce projet met en place un systeme de recommandation intelligent permettant d’associer chaque etudiant a des encadrants potentiels selon la coherence entre son sujet de PFE, sa filiere, ses competences et le profil des enseignants.

L’objectif principal est de produire, pour chaque etudiant, une liste de recommandations pertinentes et ordonnees, en tenant compte a la fois de la structure academique et de la proximite metier entre les profils.

Principe general
Le systeme repose sur une approche hybride combinant :

des informations structurelles issues de la base de donnees
des representations textuelles enrichies des etudiants et des encadrants
des mesures de similarite semantique
des regles de compatibilite metier
un score final de classement
Donnees utilisees
Le notebook exploite plusieurs fichiers CSV exportes depuis la base :

clean_users.csv
clean_teachers.csv
clean_students_predefined_lists.csv
clean_groups.csv
clean_sectors.csv
clean_departments.csv
clean_cv_skills.csv
clean_cv_skill_users.csv
clean_stages.csv
clean_stage_types.csv
Ces fichiers permettent de reconstruire les profils et les relations entre etudiants, groupes, secteurs, departements, enseignants et stages.

Identification des profils
Encadrants
Pour les enseignants, la specialite est recuperee directement depuis la table des enseignants, notamment via :

la specialite metier
le departement de rattachement
les competences


Etudiants
Pour les etudiants, la filiere est reconstruite a partir de la chaine suivante :

groupe -> secteur -> departement
Le profil etudiant est ensuite enrichi par :

le sujet de PFE
les competences
les informations descriptives disponibles


Construction de la recommandation
Le systeme compare chaque etudiant aux encadrants compatibles, en utilisant plusieurs signaux :

compatibilite du departement
proximite entre competences
similarite semantique entre le sujet et le profil de l’enseignant
proximite avec la specialite de l’enseignant
experience de l’enseignant sur des sujets similaires
disponibilite de l’enseignant

emb_sim : similarite semantique entre profil etudiant et profil enseignant
skill_jaccard : chevauchement entre les competences
specialite_sim : proximite entre le sujet et la specialite de l’encadrant
historique_sim : proximite avec les anciens sujets encadres
availability : disponibilite de l’enseignant
Sortie du systeme
Pour chaque etudiant, le notebook genere :

un classement des meilleurs encadrants
un top 5 final
un score de recommandation
des raisons explicatives associees a chaque proposition