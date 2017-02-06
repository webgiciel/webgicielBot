# webgicielBot
Robot numérique de mutualisation de serveur.<br>
L'internet d'aujourd'hui se transforme en minitel. Nous sommes de plus en plus observé, écouté, suivie, pour tout dire étudié par de grands groupes industriels. Ils se servent de nos données pour concevoir une intelligence artificielle leur permettant de mieux nous manipuler.<br>
Le projet du webgicielBot est de revenir aux valeurs de liberté de l'origine de l'internet, en donnant des outils nécessaires et suffisants à des propriétaires de serveurs.<br>
<br>
<b>Prérequis :</b><br>
<ul>
<li>un serveur de type Debian 8</li>
<li>un nom de domaine rattaché</li>
<li>copier l'ensembles des fichiers sur le serveur</li>
<li>initialiser les tables SQL</li>
</ul><br>
<br>
<b>Objectifs :</b><br>

Version 1.0
- un site public modifiable par le site d'administration
- un site d'administration en https
- autant de sites public alias que d'utilisateurs modifiable par le site d'administration

Version ultérieur
- mettre un compte à rebours sur le bouton des tentatives d'identification
- mettre un bloqueur au formulaire d'oubli des identifiants après 3 essais

Plusieurs niveaux d'utilisateurs sont possibles :
- Propriétaire du serveur
- Developpeur et/ou administrateur
- Modérateurs
- Membres
- Invités

<h2>Commençons par faire le module d'entrée du site d'administration</h2>

<b>A. Fonctionnalités de la page d'entrée du site d'administration</b>
- skip l'identification si la session est reconnue
- mouche le passage
- formulaire d'identification
	- bloque le formulaire s'il il y a eu plus de 3 tentatives en 15 minutes + compte à rebours
- script jquery des fonctionnalités du formulaire
	- touche enter sur les inputs
	- btn annule
	- btn login
- ajax du traitement du formulaire d'identification + protection sql injection
	- init Session + dirige vers page welcome
	- mouche les echecs à l'identification
		- div message erreur + compte à rebours
		- bouton [identifiant oublié]
		- formulaire de récupération des identifiants
		- script jquery des fonctionnalités du formulaire
			- touche enter sur le input
			- btn annule
			- btn recup
		- ajax du traitement du formulaire de récupération des identifiants
			- mouche les echecs à l'identification + message error
			- envoi un mail + lien avec clé courte

<b>B. Page de recréation de mot de passe en cas d'oubli</b>
- si la clef est valide
	- recupère les infos user
	- affiche le formulaire de nouveau password
		- verifie les conditions
			- pass > 4 car
			- pass2 = pass1
		- ajax du traitement du formulaire de nouveau password + protection sql injection
			- recupere l id de la key
			- recupere les infos user avec l id
			- crypt key
			- save new mot de passe
			- desactive clé courte new pass
			- envoi mail changement pass ok
- sinon la clef est invalide
	- message clé désactivée


<b>Page welcome de l'administration</b>
- redirectionne sur la page d'identification si la session n'est pas reconnue
- mouche le passage
- barre de menu adapté au niveau de l'utilisateur

<b>nécessite table SQL</b>
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

oubli
	- id
	- ip
	- pseudo
	- cle
	- actif
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



	
