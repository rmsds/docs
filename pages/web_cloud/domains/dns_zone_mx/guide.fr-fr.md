---
title: Configurer un enregistrement MX
excerpt: Découvrez comment configurer un enregistrement MX sur votre nom de domaine chez OVHcloud
updated: 2023-08-30
---

## Objectif

L'enregistrement MX permet de relier un nom de domaine au serveur de sa plateforme e-mail. Il est indispensable pour que le service e-mail de l'expéditeur puisse atteindre celui du destinataire.

**Découvrez comment configurer un enregistrement MX pour votre nom de domaine chez OVHcloud.**

## Prérequis

- Disposer d'un accès à la gestion de la zone DNS du nom de domaine concerné depuis l'[espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
- Être connecté à votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
- Le nom de domaine concerné doit utiliser la configuration OVHcloud (c'est à dire les serveurs DNS d'OVHcloud).
- Disposer d'une offre MX Plan (incluse dans l'offre d’[hébergement web](https://www.ovhcloud.com/fr/web-hosting/), l'[hébergement gratuit 100M](https://www.ovhcloud.com/fr/domains/free-web-hosting/) ou l'offre MX Plan commandée séparément), une de nos [offres e-mail OVHcloud](https://www.ovhcloud.com/fr/emails/), ou un service e-mail externe.

> [!primary]
>
> - Si votre nom de domaine n'utilise pas les serveurs DNS d'OVHcloud, vous devez réaliser la modification des enregistrements MX depuis l'interface du prestataire gérant la configuration de votre nom de domaine.
>
> - Si votre nom de domaine est déposé chez OVHcloud, vous pouvez vérifier si ce dernier utilise notre configuration OVHcloud dans votre [espace client](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), dans la partie `Serveurs DNS`{.action}, une fois positionné sur le domaine concerné, dans l'onglet `informations générales`{.action}. Si la mention `Actif` est présente sous « **serveurs DNS** », vous utilisez bien les serveurs DNS OVHcloud.
>
> ![email](images/email-dns-conf-mx00.png){.thumbnail}

## En pratique

### Comprendre le rôle des enregistrements MX 

Les enregistrements MX (**M**ail e**X**change) permettent de relier votre nom de domaine aux serveurs e-mail de réception attachés à votre service e-mail. Nous allons nous appuyer sur un exemple.

Lorsque l'adresse **sender@otherdomain.ovh** envoie un e-mail vers **contact@mydomain.ovh**, le serveur d'envoi e-mail (**Outgoing mail server**) va :
- **(1)** interroger la zone DNS du nom de domaine **mydomain.ovh** et lire les enregistrements **MX**.
- **(2)** transmettre l'e-mail vers l'URL de l'enregistrement **MX** lu.

![email](images/email-dns-conf-mx01.png){.thumbnail}

L'e-mail sera envoyé vers la cible **mx0.mail.ovh.net** qui est précédée de la valeur **0**. Cette valeur est appelée priorité. La plus faible valeur est interrogée en premier et la plus élevée en dernier. Cela signifie que la présence de plusieurs enregistrements permet de pallier une absence de réponse de l'enregistrement MX ayant la plus faible priorité.

Vous pouvez paramétrer plusieurs enregistrements MX pour un même nom de domaine. Il est alors nécessaire de définir un numéro de priorité pour chacun d'entre eux. Les enregistrements MX sont interrogés par ordre croissant, du numéro le plus faible au plus élevé, jusqu'à obtenir une réponse du serveur de réception.

> [!warning]
>
> De manière générale, **modifier les enregistrements MX dans la zone DNS de son nom de domaine est une manipulation délicate** : réaliser une mauvaise manipulation peut rendre impossible la réception des e-mails sur vos adresses. Nous vous invitons à être vigilant lors de la réalisation de cette manipulation.
> En cas de doute, nous vous conseillons de faire appel à un [prestataire spécialisé](https://partner.ovhcloud.com/fr/directory/).

### Valeurs de la configuration MX OVHcloud <a name="mxovhcloud"></a>

Retrouvez ci-dessous la configuration MX OVHcloud à utiliser pour nos solutions MX Plan (seule ou incluse dans une offre d’[hébergement web OVHcloud](https://www.ovhcloud.com/fr/web-hosting/)), [E-mail Pro](https://www.ovhcloud.com/fr/emails/email-pro/) et [Exchange](https://www.ovhcloud.com/fr/emails/). Nos serveurs e-mail disposent d'un antispam et d'un antivirus intégré.

|Domaine|TTL|Type d'enregistrement|Priorité|Cible|
|---|---|---|---|---|
|*laisser vide*|3600|MX|1|mx0.mail.ovh.net.|
|*laisser vide*|3600|MX|5|mx1.mail.ovh.net.|
|*laisser vide*|3600|MX|50|mx2.mail.ovh.net.|
|*laisser vide*|3600|MX|100|mx3.mail.ovh.net.|
|*laisser vide*|3600|MX|200|mx4.mail.ovh.net.|

Ces enregistrements MX doivent être configurés dans la zone DNS de votre nom de domaine.

### Configurer un enregistrement MX dans une zone DNS OVHcloud

Pour créer ou modifier les enregistrements MX dans la configuration OVHcloud de votre nom de domaine, connectez-vous à votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). Rendez-vous dans la section `Noms de domaine`{.action}, cliquez sur le domaine concerné puis rendez-vous dans l'onglet `Zone DNS`{.action}.

Le tableau affiche la configuration OVHcloud de votre nom de domaine. Chaque ligne correspond à un enregistrement DNS.

Dans un premier temps, nous vous invitons à vérifier si des enregistrements MX existent déjà dans la configuration DNS OVHcloud de votre nom de domaine, en vous aidant de la liste de filtrages située au dessus du tableau de votre zone DNS.<br>
Sélectionnez le type **MX** puis validez pour n'afficher que les entrées DNS MX de votre zone DNS. Aidez-vous de la capture d'écran ci-dessous.

![dnsmxrecord](images/mx-records-dns-zone.png){.thumbnail}

- Si des enregistrements MX existent déjà et que vous souhaitez les modifier, cliquez sur le bouton `...`{.action} à droite de chaque ligne du tableau concernée puis cliquez sur `Modifier l'entrée`{.action}.
- Si aucun enregistrement MX n'est présent, cliquez sur le bouton `Ajouter une entrée`{.action} à droite du tableau puis choisissez `MX`{.action}. Complétez les informations demandées en fonction de la solution e-mail choisie :

**Si vous disposez d'une solution e-mail OVHcloud**, reportez-vous aux informations données à l'étape « [Connaître la configuration MX d'OVHcloud ](#mxovhcloud) ».

![dnsmxrecord](images/mx-records-dns-zone-modif.png){.thumbnail}

Une fois les informations complétées, finalisez les étapes puis cliquez sur `Valider`{.action}.

**Si vous disposez d'une autre solution e-mail**, reportez-vous aux informations communiquées par votre fournisseur de service e-mail.

> [!primary]
>
> La modification nécessite un temps de propagation de 4 à 24 heures avant d’être pleinement effective.
>

## Aller plus loin

[Généralités sur les serveurs DNS](/pages/web_cloud/domains/dns_server_general_information)

[Éditer une zone DNS OVHcloud](/pages/web_cloud/domains/dns_zone_edit)

[Configurer un enregistrement SPF sur son nom de domaine](/pages/web_cloud/domains/dns_zone_spf)

[Configurer un enregistrement DKIM](/pages/web_cloud/domains/dns_zone_dkim)

Pour des prestations spécialisées (référencement, développement, etc), contactez les [partenaires OVHcloud](https://partner.ovhcloud.com/fr/).

Si vous souhaitez bénéficier d'une assistance à l'usage et à la configuration de vos solutions OVHcloud, nous vous proposons de consulter nos différentes [offres de support](https://www.ovhcloud.com/fr/support-levels/).

Échangez avec notre communauté d'utilisateurs sur <https://community.ovh.com>.
