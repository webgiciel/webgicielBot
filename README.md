# webgicielBot
Robot numérique de mutualisation de serveur.<br>
L'internet d'aujourd'hui se transforme en minitel. Nous sommes de plus en plus observé, écouté, suivie, pour tout dire étudié par de grands groupes industriels. Ils se servent de nos données pour concevoir une intelligence artificielle leur permettant de mieux nous manipuler.<br>
Le projet du webgicielBot est de revenir aux valeurs de liberté de l'origine de l'internet, en donnant des outils nécessaires et suffisants à des propriétaires de serveurs.<br>

<b>Prérequis :</b><br>
<ul>
<li>un serveur de type Debian 8</li>
<li>un nom de domaine rattaché</li>
<li>copier l'ensembles des fichiers sur le serveur</li>
<li>initialiser les tables SQL</li>
</ul>

Objectifs :

Version 1.0
- un site public modifiable par le site d'administration
- un site d'administration en https
- autant de sites public alias que d'utilisateurs modifiable par le site d'administration

Plusieurs niveaux d'utilisateurs sont possibles :
- Propriétaire du serveur
- Developpeur et/ou administrateur
- Modérateurs
- Membres
- Invités

Commençons par faire la page d'entrée du site d'administration :

<b>Fonctionnalités de la page d'entrée du site d'administration</b>
- skip l'identification si la session est reconnue
- mouche le passage
- formulaire d'identification
	- bloque le formulaire s'il il y a eu plus de 3 tentatives en 15 minutes + compte à rebours
- script jquery des fonctionnalités du formulaire
	- touche enter sur les inputs
	- btn annule
	- btn login
- ajax du traitement du formulaire d'identification + protection sql injection
- mouche les echecs à l'identification
- div message erreur + compte à rebours
- bouton [identifiant oublié]
 formulaire de récupération des identifiants
 ajax du traitement du formulaire de récupération des identifiants
 div erreur
 - init Session + dirige vers page welcome

Page welcome de l'administration
- redirectionne sur la page d'identification si la session n'est pas reconnue
- mouche le passage
- barre de menu adapté au niveau de l'utilisateur

nécessite table SQL
users
	- id
	- pseudo
	- pass (crypté)
	- mail
	- niveau
	- actif
	- idParrain
	- dateCrea
	- dateModif

passages
	- id
	- ip
	- os
	- langue
	- quoi
	- quand

passagesAdmin
	- id
	- userId
	- ip
	- os
	- langue
	- quoi
	- quand

passagesAdminError
	- id
	- ip
	- os
	- langue
	- login
	- pass
	- quoi
	- quand

necessite des classes PHP pour les traitements
	- bot.bdd.php
		- connectionInsertInto($query, $donnees)
	- bot.htmlElement.php
		- afficheDoctype($niv)
		- afficheHeadHtml()
		- afficheOuvertureBody()
		- afficheFermetureBody()
		- afficheFermetureHtml()
		- afficheOuvertureContainer($val)
		- afficheFermetureContainer()
	- bot.mouche.php
		- passage($quoi)
		- passageAdmin($quoi)
        - bot.user.php
		- cryptPass($pass)
		- initKey($pseudo, $id, $mail)
		- initSession($id, $pseudo, $contact, $niveau)
		- decoupeKey($key)
		- testSessionValide()
		- testUser()
		- skipIdentification()



	
