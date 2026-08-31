# Fiche projet — Équipe 16

> Livrable L2 · Jalon J1 (samedi 29 août 2026) · validée par l'encadreur référent.
> Aucune fabrication n'est autorisée avant la validation de ce jalon.

## 1. Titre et accroche

**Détecteur de porte restée ouverte.** Un dispositif à trois composants qui transforme une consigne de sécurité affichée sur la porte en un contrôle effectif et automatique, sans surveillance humaine permanente.

## 2. Besoin et bénéficiaires

Le local à produits chimiques, la réserve, la salle informatique : plusieurs portes de l'établissement ne doivent jamais rester entrebâillées, pour des raisons de sécurité (exposition, vol, intégrité du matériel) ou de confidentialité des accès. Aujourd'hui, ce contrôle repose uniquement sur la vigilance du personnel.

Bénéficiaires directs : le chef de travaux et le responsable de la sécurité de l'établissement, qui définissent avec les élèves la temporisation acceptable et la consigne associée. Élèves concernés : classe de technologie / sciences de l'ingénieur, niveau 1 (aucun prérequis au-delà du socle commun), effectif d'un binôme à un petit groupe pour la conception, avec une séance dédiée en classe entière pour l'analyse du besoin de sécurité (recensement des locaux sensibles avec le chef de travaux). Établissement d'accueil : l'établissement scolaire disposant des locaux sensibles concernés et du fablab de fabrication.

## 3. Objectifs d'apprentissage

Trois objectifs observables rattachés au programme officiel, chapitre cité.

1. Mesurer un état physique binaire (porte ouverte/fermée) à l'aide d'un capteur magnétique et exploiter cette mesure dans une logique de décision temporisée (chapitre « capter et mesurer une grandeur physique »).
2. Concevoir une chaîne de commande simple associant un capteur, un microcontrôleur en veille basse consommation et un actionneur (buzzer, émission radio), en justifiant les choix de composants (chapitre « chaîne d'énergie et chaîne d'information »).
3. Conduire une analyse de besoin de sécurité avec un acteur réel de l'établissement (recensement des locaux, négociation d'une temporisation, rédaction d'une consigne), et en tirer un réglage technique justifié (chapitre « analyse du besoin et cahier des charges »).

## 4. Description du dispositif

Ce que l'objet fait : un contact magnétique de type reed, monté sur le dormant de la porte, informe une carte électronique compacte de l'état de la porte. Au-delà d'une minute d'ouverture continue, un signal sonore progressif se déclenche localement, puis une alerte est répétée à distance vers un point de surveillance ; chaque événement est journalisé avec sa durée pour permettre une analyse hebdomadaire.

Ce que l'élève fait avec : il installe le contact sur la porte de son local sensible, ajuste la temporisation d'alerte en observant l'usage réel du local, et consulte le journal hebdomadaire pour objectiver la fréquence et la durée des ouvertures prolongées.

Croquis ou esquisse annotée : à verser dans `docs/medias/` (vue éclatée du boîtier deux parties, position du contact reed sur le dormant et de l'aimant sur le vantail).

## 5. Architecture technique pressentie

- **Capteurs** : contact magnétique reed monté sur le dormant, aimant sur le vantail avec cale d'alignement.
- **Actionneurs** : buzzer local à alarme progressive (bips espacés puis continus selon la durée d'ouverture).
- **Liaison** : émission radio 433 MHz (courte portée), paquet identifiant le local et la durée, répété toutes les 30 secondes tant que la porte reste ouverte au-delà du seuil.
- **Application** : aucune application mobile ; réception et journalisation sur un point central simple (recepteur RF + microcontrôleur + mémoire de journalisation), consultable localement.
- **Procédés de fabrication envisagés** (trois procédés distincts, exigence ET-FAB-02) :
  1. Gravure au laser fibre MOPA (xTool F2 Ultra) pour la carte électronique, très compacte.
  2. Impression 3D pour le boîtier en deux parties clipsées.
  3. Découpe laser pour la cale d'alignement de l'aimant et l'étiquette d'identification du local (gravée au laser fibre).

## 6. Rôle des élèves

Position sur le continuum POUR / AVEC / PAR : le dispositif est conçu **AVEC** les élèves pour la partie analyse du besoin (recensement des locaux sensibles et négociation de la temporisation menés conjointement avec le chef de travaux, qui reste décisionnaire sur les locaux et les consignes finales), et réalisé **PAR** les élèves pour l'ensemble de la conception technique et de la fabrication (extension PAR décrite, exigence EP-03) : choix et câblage des composants, programmation du firmware, gravure et assemblage des cartes et boîtiers, tests de validation. Aucune étape de fabrication n'est déléguée à un tiers extérieur à l'équipe, hormis la vérification du câblage électrique par un adulte qualifié lorsque cela s'avère pertinent pour la sécurité.

## 7. Ancrage réseau et implantation

Lab de rattachement : fablab de l'établissement (CRIT ou établissement, à préciser selon l'équipe). Lieu d'usage : les locaux sensibles identifiés lors de l'analyse du besoin (local à produits chimiques, réserve, salle informatique, ou sous-ensemble retenu par l'équipe). Conditions matérielles de la salle : accès à une prise pour le point central de réception (pas de contrainte d'alimentation autonome à ce niveau), portée radio à vérifier entre chaque local et le point central lors de l'installation.

## 8. Périmètre

| | Contenu |
|---|---|
| Dans la v1.0 (Socle) | Un poste de porte fonctionnel (contact reed, carte gravée, alarme locale progressive, émission RF) ; un point de réception central journalisant les événements (local, durée) ; temporisation réglable en dur lors de la programmation. |
| En option (Avancé / Expert) | Déploiement sur plusieurs locaux avec identifiants distincts ; interface de consultation du journal hebdomadaire plus lisible (affichage ou export) ; réglage de la temporisation sans reprogrammation (potentiomètre ou interrupteurs de configuration). |
| Explicitement exclu | Toute fonction de verrouillage ou de contrôle d'accès automatisé de la porte ; toute notification via un service en ligne ou une application mobile ; toute action à distance sur la porte elle-même (le dispositif alerte, il n'agit pas sur l'ouvrant). |

## 9. Risques et parades

| Risque | Type | Parade |
|---|---|---|
| Temporisation trop courte, alertes perçues comme intempestives, dispositif débranché par les usagers | technique | Régler le seuil par observation réelle du local avant la mise en service définitive ; rendre la valeur facilement modifiable lors des premiers jours d'usage |
| Délai insuffisant pour fabriquer et tester avant le jalon suivant | calendrier | Prioriser un seul poste de porte fonctionnel de bout en bout (v1.0 socle) avant d'envisager le déploiement multi-locaux (option) |
| Analyse du besoin superficielle si le chef de travaux n'est pas disponible en temps voulu | pédagogique | Planifier l'entretien avec le chef de travaux dès le lot Cadrage, avec une question de repli (temporisation par défaut de 1 minute, conforme à l'intention initiale) si l'entretien est reporté |

## 10. Budget matière estimé

Estimation pour un poste de porte complet (contact reed, microcontrôleur basse consommation, buzzer, module RF, accumulateur LiPo et module de charge, matière première carte/boîtier/cale) : de l'ordre de 12 000 à 18 000 FCFA par poste selon les composants retenus localement. Pour un déploiement à 3 postes plus le point central, l'ensemble reste compatible avec la dotation plafond de 60 000 FCFA, en privilégiant des composants du commerce local et en évitant la duplication de la mémoire de journalisation (centralisée sur le point de réception).

## 11. Licences et diffusion

Licence matérielle proposée : CERN-OHL-S (ou équivalent open hardware) pour les schémas et fichiers de fabrication de la carte et des boîtiers ; licence logicielle proposée : MIT pour le firmware. Motivation : permettre à d'autres équipes ou établissements de reproduire et d'adapter le dispositif à leurs propres locaux sensibles, dans la continuité de la démarche de projet reproductible. Accord de l'équipe pour la mise en avant réseau : à recueillir auprès de l'équipe avant publication.

## Exemptions demandées

- [x] ET-FAB-06 (moulage) — justification : le dispositif ne comporte aucune pièce nécessitant un moulage résine/silicone ; les boîtiers et cales sont entièrement couverts par l'impression 3D et la découpe laser, procédés qui satisfont déjà l'exigence de diversité de fabrication (ET-FAB-02, trois procédés distincts) sans qu'un moulage apporte de valeur fonctionnelle supplémentaire à ce dispositif.
- [x] ET-MEC-01 (fonction motorisée) — justification : le dispositif est un capteur de présence à alerte (contact reed + buzzer + émission radio), sans aucun mécanisme mobile à motoriser ; il agit uniquement par signalisation sonore et radio, jamais par une action mécanique sur la porte elle-même, ce qui exclut naturellement toute fonction motorisée pertinente pour ce projet.