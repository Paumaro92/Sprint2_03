Òptica "Cul d'Ampolla" - Gestió amb MongoDB
📖 Descripció
Aquest projecte consisteix en el disseny i la creació d'una base de dades NoSQL amb MongoDB per a la gestió d'una òptica anomenada "Cul d'Ampolla". L'objectiu és modelar la informació de proveïdors, ulleres, clients i vendes de manera eficient, tenint en compte que l'accés a les dades ha d'estar optimitzat per a diferents interfícies d'usuari.

El model de dades documental de MongoDB és ideal per a aquest cas, ja que permet estructures flexibles i niades que s'adapten a les necessitats de l'aplicació.

Taula de continguts
Model de Dades

Estructura de la Base de Dades (Exercicis)

Exercici 1: Visió del Client

Exercici 2: Visió de les Ulleres

Tecnologies Utilitzades


🗂️ Model de Dades
El sistema ha de gestionar les següents entitats principals:

Proveïdors: Emmagatzema la informació de contacte i fiscal de cada proveïdor d'ulleres.

Camps: Nom, adreça (carrer, número, pis, porta, ciutat, CP, país), telèfon, fax i NIF.

Ulleres: Conté tots els detalls tècnics i comercials de cada parell d'ulleres.

Camps: Marca, graduació dels vidres, tipus de muntura (flotant, pasta, metàl·lica), color de la muntura, color dels vidres i preu.

Clients: Guarda la informació personal i de contacte dels clients.

Camps: Nom, adreça postal, telèfon, correu electrònic, data de registre i, opcionalment, el client que l'ha recomanat.

Vendes: Registra cada transacció, associant un client, unes ulleres i un empleat.

Camps: Empleat que ha realitzat la venda i data/hora de la venda.

🏗️ Estructura de la Base de Dades (Exercicis)
MongoDB organitza les dades en documents flexibles (en format BSON/JSON). A continuació es presenten dos possibles dissenys, cadascun optimitzat per a una interfície d'usuari diferent, tal com demanen els exercicis.

Exercici 1: Disseny orientat a la interfície del client
Per optimitzar una interfície on el client consulta el seu historial, el disseny se centra a agrupar tota la informació rellevant en un únic lloc. Això redueix les consultes a la base de dades i accelera la càrrega del perfil d'usuari.

Lògica principal: El document del Client és el nucli.

Estructura:

Es crea un document principal per a cada client.

Dins de cada document de client, s'hi incrusta (embed) un array anomenat compres.

Cada element d'aquest array representa una venda i conté tota la informació de les ulleres comprades en aquella transacció (marca, graduació, preu, etc.), juntament amb la data de la venda i l'empleat que la va atendre.

Avantatge: En una sola consulta per obtenir un client, tenim accés a totes les seves dades i al seu historial de compres complet, ideal per mostrar a la seva àrea personal.

Exercici 2: Disseny orientat a la interfície de les ulleres
Si la interfície principal se centra en la gestió del catàleg d'ulleres (per a un empleat, per exemple), el disseny canvia. En aquest model, les dades estan més distribuïdes i s'utilitzen referències per connectar la informació.

Lògica principal: El document de les Ulleres és el protagonista.

Estructura:

Es crea un document principal per a cada parell d'ulleres del catàleg, amb totes les seves característiques tècniques.

Aquest document conté una referència (utilitzant el seu _id) al document del proveïdor que les subministra.

Quan es produeix una venda, s'afegeix informació al document de les ulleres, com la data de venda, l'empleat i una referència al document del client que les ha comprat.

Avantatge: Facilita la cerca i gestió de l'inventari d'ulleres. Permet consultar ràpidament quin proveïdor subministra un model concret o si unes ulleres han estat venudes i a qui, sense haver de carregar tota la informació dels clients.

🛠️ Tecnologies Utilitzades
Base de Dades: MongoDB

GUI Recomanada: MongoDB Compass per a la visualització i gestió de dades.