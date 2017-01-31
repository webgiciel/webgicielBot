# webgicielBot
Robot numérique de mutualisation de serveur

Prérequis :
- un serveur de type Debian 8
- un nom de domaine rattaché

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
- mouche le passage
- formulaire d'identification
- script jquery des fonctionnalités du formulaire
	- touche enter sur les inputs
	- btn annule
	- btn login
- ajax du traitement du formulaire d'identification + protection sql injection
 mouche les echecs à l'identification
 div erreurs
 bouton [identifiant oublié]
 formulaire de récupération des identifiants
 ajax du traitement du formulaire de récupération des identifiants
 div erreur
 dirige vers page welcome

nécessite table users
	id
	pseudo
	pass (crypté)
	mail
	niveau
	actif
	idParrain
	dateCrea
	dateModif

et table passages
	id
	ip
	os
	langue
	quoi
	quand

necessite des classes PHP pour les traitements
	- bot.bdd.php
		- connectionInsertInto($query, $donnees)
	- bot.htmlElement.php
		- doctype($niv)
		- htmlHeader()
	- bot.mouche.php
		- mouche($quoi)
        - formulaireIdentification()


	
