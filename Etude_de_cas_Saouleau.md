# But de la Manip

Positionner des icones automatiquement  sur un tableau dans un cadre donné (exemple 1200/600 px).

Cadre
Ce cadre doit avoir des dimensions max en largeur  et un rapport (L/H fixe ac).. Les dimensions de ce cadre sont fonction de la zone allouée à la présentation générale du document sur le site Saouleau.

Fond (Tableau)
Ce tableau est généralement une carte géographique mondiale (rognée aux zones arctique et antarctique) mais peut être aussi une zone régionale (Caraïbes ou méditerranée ou tout autre zone).
Il faut donc prévoir dès maintenant n tableaux.                                                                                         
Icônes
Les Icônes à créer et positionner sont pour :
	des Points MAP  (actuellement)
	des Lieux de plongée (nouveauté)
	des info Météo (nouveauté + f(saison)
	celles utilisées déjà dans le site (site ref, Google, etc) en consultation
	Autres idée d’utilisation possible.

Ces travaux utiliseront 3 tables reliées entre elles. 
Une table z_zones (Océans) qui indiquera pour chaque ligne un océan ou une partie d’un océan (exemple océan arctique ou Atlantique centre ouest,…)
-- Structure de la table `z_zones`
CREATE TABLE `z_zones` (  `id` int(4) NOT NULL,  `zone` varchar(30) DEFAULT NULL) ENGINE=InnoDB DEFAULT CHARSET=latin1;
Une table z_map donnant la liste des positions de grandes zones de plongées dans le monde et présentant une certaine homogénéité.  Chacune de ces lignes pointera sur une ligne de la table z_zones via le champ id_zone. Plusieurs points-MAP pour une ligne de z_zones.
Exemple :
--
-- Structure de la table `z_map`
--
CREATE TABLE `z_map` (  `id` int(11) NOT NULL,  `id_zone` int(11) NOT NULL,  `nom_map` varchar(255) NOT NULL,  `x_map` int(11) NOT NULL,  `y_map` int(11) NOT NULL) 


Une table photos contenant les lieux des  plongées effectuées par les membres Saouleau  et renseignés lors des soumissions des photos (Pays/Région/Ville si nécessaire). Chacun de ces lieux (photo) pointera sur un Point-MAP (champ id_map). Ces liens seront effectués lors de l’analyse de soumission des photos.
-- Structure de la table `z_photos`
 
CREATE TABLE `z_photos` (  `id` int(11) NOT NULL,  `id_cat` int(11) NOT NULL,  `id_fam_site` varchar(20) DEFAULT NULL,  `genre` varchar(20) NOT NULL,  `espece` varchar(20) NOT NULL,  `s_espece` varchar(20) DEFAULT NULL,  `rang` varchar(2) NOT NULL,  `rg` int(11) NOT NULL,  `id_sexe` varchar(1) NOT NULL,  `rem` int(4) DEFAULT NULL,  `affichage` int(2) DEFAULT '99',  `commentaire` varchar(50) DEFAULT NULL,  `lieu` varchar(60) NOT NULL,  `annee` varchar(4) DEFAULT NULL,  `photographe` varchar(2) DEFAULT NULL,  `id_zone` int(11) NOT NULL,  `id_map` int(11) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;
Outil(s)  à réaliser par moi-même

Sur une image (carte)  de dimensions données (ex  1800 pixels/ 1000 pixels),
- positionner (à l’aide de la souris)  une icône (étoile) sur la carte et enregistrer dans la table z_map
- le nom de ce point-MAP
- les coordonnées relatives à l’image obtenues par le positionnement
- relier ce point à la table z_zones (Océans).
Ces points devront être 
Cliquables pour accéder à une page d’informations à définir ultérieurement.
D’une couleur différente suivant que des lieux (photos) sont rattachés à ce point-MAP ou non
Vérifier qu’en relisant la table Point-MAP l’icônes se positionnent correctement.

Pouvoir modifier la table z_map
En repositionnant un point (coordonnées),
En modifiant son nom,
Voire en supprimant ce point-MAP (analyser la façon en tenant compte des liens éventuels provenant de photos existantes)
Détacher un lieu de plongée d’un point-MAP et le réaffecter à un autre Point-MAP
