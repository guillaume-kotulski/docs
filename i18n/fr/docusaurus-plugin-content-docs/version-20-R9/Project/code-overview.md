---
id: code-overview
title: Méthodes et classes
---

Le code 4D utilisé dans votre projet est écrit dans des [méthodes](../Concepts/methods.md) et des [classes](../Concepts/classes.md).

L'IDE de 4D vous offre diverses fonctionnalités pour créer, modifier, exporter ou supprimer votre code. Vous utiliserez généralement l'[éditeur intégré de code 4D](../code-editor/write-class-method.md) pour travailler avec votre code. Vous pouvez également utiliser d'autres éditeurs tels que **VS Code**, pour lesquels l'extension [4D-Analyzer](https://github.com/4d/4D-Analyzer-VSCode) est disponible.

## Créer des méthodes

Une méthode dans 4D est stockée dans un fichier **.4dm** situé dans le dossier approprié du dossier [`/Project/Sources/`](../Project/architecture.md#sources).

Vous pouvez créer [plusieurs types de méthodes](../Concepts/methods.md) :

- Tous les types de méthodes peuvent être créés ou ouverts à partir de la fenêtre de l'**Explorateur** (à l'exception des méthodes objet qui sont gérées à partir de l'[éditeur de formulaires](../FormEditor/formEditor.md)).
- Les méthodes projet peuvent également être créées ou ouvertes à partir du menu **Fichier** ou de la barre d'outils (**Nouveau/Méthode...** ou **Ouvrir/Méthode...**) ou à l'aide de raccourcis dans la [fenêtre de l'éditeur de code](../code-editor/write-class-method.md#shortcuts).
- Les triggers peuvent également être créés ou ouverts à partir de l'éditeur de Structure.
- Les méthodes formulaire peuvent également être créées ou ouvertes à partir de l'[éditeur de formulaires](../FormEditor/formEditor.md).

## Créer des classes

Une classe utilisateur dans 4D est définie par un fichier de méthode spécifique (**.4dm**), stocké dans le dossier [`/Project/Sources/Classes/`](../Project/architecture.md#sources). Le nom du fichier est le nom de la classe.

Vous pouvez créer un fichier de classe à partir du menu ou de la barre d'outils **Fichier** (**Nouveau/Classe...**) ou dans la page **Méthodes** de la fenêtre de l'**Explorateur** .

Pour plus d'informations, reportez-vous à la section [Classes](../Concepts/classes.md).

## Supprimer des méthodes ou des classes

Pour supprimer une méthode ou une classe existante, vous pouvez :

- sur votre disque, supprimer le fichier *.4dm* du dossier "Sources",
- dans l'explorateur de 4D, sélectionnez la méthode ou la classe et cliquez sur ![](../assets/en/Users/MinussNew.png) ou choisissez **Déplacer vers la corbeille** dans le menu contextuel.

> Pour supprimer une méthode objet, choisissez **Supprimer la méthode objet** dans l'[éditeur de formulaires](../FormEditor/formEditor.md) (menu **Objet** ou menu contextuel).

## Importer et exporter le code

Vous pouvez importer et exporter une méthode ou le code d'une classe sous la forme d'un fichier. Ces commandes se trouvent dans le menu **Méthode** de l'[éditeur de code](../code-editor/write-class-method.md).

- Lorsque vous sélectionnez la commande **Exporter la méthode...** , une boîte de dialogue standard d'enregistrement de fichier apparaît, vous permettant de choisir le nom, l'emplacement et le format du fichier d'export (voir ci-dessous). Comme pour l'impression, l'export ne tient pas compte de l'état contracté des structures de code et le code entier est exporté.
- Lorsque vous sélectionnez la commande **Importer la méthode...**, une boîte de dialogue standard d'ouverture de fichier standard apparaît, vous permettant de désigner le fichier à importer. L'importation remplace le texte sélectionné dans la méthode. Pour remplacer une méthode existante par une méthode importée, il suffit de sélectionner l’ensemble du contenu de la méthode avant d’effectuer l’importation.

La fonction d’import/export est multi-plate-forme : une méthode exportée sous macOS peut être importée sous Windows et inversement, 4D se charge de la conversion des caractères si nécessaire.

4D peut exporter et importer les méthodes dans deux formats :

- Méthode 4D (extension *.c4d*) : Dans ce format, les méthodes sont exportées sous forme encodée. Les noms d’objets sont transformés en références (tokens). Ce format permet notamment d’échanger des méthodes entre des applications 4D et des plug-ins dans langues différentes. En revanche, il n’est pas possible de les visualiser dans un éditeur de texte.
- Texte (extension *.txt*) : Dans ce format, les méthodes sont exportées sous forme de texte uniquement. Dans ce cas, les méthodes sont lisibles à l'aide d'un éditeur de texte standard ou d'un outil de contrôle de sources.

## Propriétés des méthodes projet

Après avoir créé une méthode projet, vous pouvez la renommer et modifier ses propriétés. Les propriétés des méthodes projet définissent principalement leurs conditions d’accès et de sécurité (accès par les utilisateurs, les serveurs intégrés ou les services) ainsi que leur mode d'exécution.

Les autres types de méthodes n'ont pas de propriétés spécifiques. Leurs propriétés sont liées à celles des objets auxquels elles sont attachées.

Pour afficher la boîte de dialogue **Propriétés de la méthode** pour une méthode projet, vous pouvez soit :

- dans l'[éditeur de code](../code-editor/write-class-method.md), sélectionnez la commande **Propriétés de la méthode...** dans le menu **Méthode**,
- ou dans la page **Méthodes** de l'Explorateur, **clic droit** sur la méthode projet et sélectionner **Modifier les propriétés** dans le menu contextuel ou dans le menu d'options.

> Une fonction de paramétrage global vous permet de modifier une propriété pour tout ou partie des méthodes projet en une seule opération (voir [Modifier attributs globalement](#modifier-attributs-globalement)).

### Nom

Vous pouvez changer le nom d'une méthode projet dans la zone **Nom** de la fenêtre **Propriétés de la méthode** ou dans l'Explorateur.

Le nouveau nom doit respecter les règles de nommage 4D (voir [Identifiants](../Concepts/identifiers.md)). Si une méthode portant le même nom existe déjà, 4D affiche un message indiquant que ce nom de méthode est déjà utilisé. Si nécessaire, 4D trie à nouveau la liste des méthodes.

:::caution

Changer le nom d'une méthode déjà utilisée dans la base de données peut invalider toutes les méthodes ou formules qui utilisent l'ancien nom de méthode et risque de perturber le fonctionnement de l'application. Changer le nom d'une méthode déjà utilisée dans la base de données peut invalider toutes les méthodes ou formules qui utilisent l'ancien nom de méthode et risque de perturber le fonctionnement de l'application. Avec cette fonction, vous pouvez mettre à jour automatiquement le nom où la méthode partout où elle est appelée dans l'environnement de développement.

Avec 4D Server, le nom de la méthode est changé sur le serveur lorsque vous avez fini de le modifier. Si plus d'un utilisateur modifie le nom de la méthode en même temps, le nom final de la méthode sera le nom spécifié par le dernier utilisateur ayant terminé de l'éditer. Vous pouvez désigner un propriétaire de la méthode pour que seuls certains utilisateurs puissent changer son nom.

:::

:::info

Les méthodes base ne peuvent pas être renommées. Il en va de même pour les triggers, les méthodes formulaire et les méthodes objet, qui sont liés à des objets et tirent leur nom de l'objet concerné.

:::

### Attributs

Vous pouvez contrôler comment les méthodes projet sont utilisées et/ou appelées dans différents contextes en utilisant des attributs. Notez que vous pouvez définir des attributs globalement pour une sélection de méthodes projet en utilisant l'Explorateur (voir la section suivante).

#### Invisible

Si vous ne voulez pas que les utilisateurs puissent exécuter une méthode projet à l'aide de la commande **Méthode...** du menu **Exécution**, vous pouvez la rendre invisible en cochant cette option. Une méthode invisible n'apparaît pas dans la boîte de dialogue d'exécution de méthode.

Lorsque vous rendez une méthode projet invisible, elle est toujours disponible pour le développeur. Elle reste listée dans l'Explorateur et de l'éditeur de code.

#### Partagée entre composants et projet hôte

Cet attribut est utilisé dans le cadre des composants. Quand il est coché, il indique que la méthode sera disponible pour les composants lorsque l'application sera utilisée comme projet hôte. A l'inverse, lorsque l'application sera utilisée en tant que composant, la méthode sera disponible pour les projets hôtes.

Pour plus d'informations sur les composants, reportez-vous au chapitre [Développer et installer des composants 4D](../Extensions/develop-components.md) .

#### Exécuter sur serveur

Cet attribut est pris en compte uniquement dans le cadre d’une application 4D en client/serveur. Lorsque cette option est cochée, la méthode du projet est toujours exécutée sur le serveur, quelle que soit la manière dont elle est appelée.

Pour plus d'informations sur cette option, reportez-vous à [Attribut Exécuter sur serveur](https://doc.4d.com/4Dv20/4D/20/Execute-on-Server-attribute.300-6330555.en.html).

### Mode d’exécution

Cette option vous permet de déclarer la méthode éligible à l'exécution en mode préemptif. Elle est décrite dans la section [Process préemptifs](../Develop/preemptive.md).

### Disponibilité

Les attributs de disponibilité précisent les services externes autorisés à appeler explicitement la méthode.

#### Web Services

Cet attribut vous permet de publier la méthode courante comme service Web accessible via des requêtes SOAP. Pour plus d’informations, reportez-vous au chapitre [Publication et utilisation de Services Web](https://doc.4d.com/4Dv20/4D/20.2/Publication-and-use-of-Web-Services.200-6750103.en.html). Lorsque cette option est cochée, l’option **Publié dans WSDL** est active.

Dans l'explorateur, les méthodes projet qui sont proposées en tant que service Web sont dotées d'une icône spécifique.

**Note :** Il n'est pas possible de publier en tant que Web service une méthode dont le nom comporte des caractères non conformes à la nomenclature XML (par exemple des espaces). Si le nom de la méthode n'est pas conforme, 4D refuse l'affectation de la propriété.

#### Publié dans WSDL

Cet attribut est actif uniquement si l'attribut "Web service" est coché. Il permet d’inclure la méthode courante dans le fichier WSDL de l’application 4D. Pour plus d’informations sur ce point, reportez-vous au paragraphe [Génération du WSDL](https://doc.4d.com/4Dv20/4D/20.2/Publishing-a-Web-Service-with-4D.300-6750334.en.html#502689).

Dans l'explorateur, les méthodes projet proposées en tant que service Web et publiées dans le WSDL sont dotées d'une icône spécifique.

#### Balises HTML et URLs 4D (4DACTION...)

Cette option permet de renforcer la sécurité du serveur Web 4D : lorsqu'elle n'est pas cochée, la méthode projet ne peut pas être exécutée via une requête HTTP contenant l'URL spéciale [4DACTION](../WebServer/httpRequests.md#4daction) utilisée pour appeler les méthodes 4D, ni les balises spéciales [4DSCRIPT, 4DTEXT et 4DHTML](../Tags/transformation-tags.md).

Dans l'explorateur, les méthodes projet ayant cet attribut sont dotées d'une icône spécifique.

Pour des raisons de sécurité, cette option est désélectionnée par défaut. Vous devez désigner individuellement chaque méthode pouvant être exécutée via les URLs et les balises spéciales.

#### SQL

Lorsqu’elle est cochée, cette option autorise l’exécution de la méthode projet par le moteur SQL de 4D. Elle est désélectionnée par défaut, ce qui signifie que, sauf autorisation explicite, les méthodes projet de 4D sont protégées et ne peuvent pas être appelées par le moteur SQL de 4D.

Cette propriété s'applique à toutes les requêtes SQL internes et externes --- exécutées via le driver ODBC, le code SQL inséré entre les balises [Begin SQL](../commands-legacy/begin-sql.md)/[End SQL](../commands-legacy/end-sql.md) ou la commande [`QUERY BY SQL`](../commands-legacy/query-by-sql.md).

**Notes :**

- Même si une méthode dispose de l’attribut “SQL”, les accès définis au niveau des propriétés de la base et des propriétés de la méthode sont pris en compte pour l’exécution de la méthode.
- La fonction ODBC **SQLProcedure** retourne uniquement les méthodes projet disposant de l’attribut "SQL".

Pour plus d’informations, reportez-vous à la section [Implémentations du moteur SQL de 4D](https://doc.4d.com/4Dv20/4D/20/4D-SQL-engine-implementation.300-6342089.en.html) in dans le manuel SQL de 4D.

#### Serveur REST

_Cette option est obsolète. L'appel de code par le biais d'appels REST n'est possible qu'avec les [fonctions de classe du modèle de données ORDA](../REST/ClassFunctions.md).\*

#### Modifier attributs globalement

La boîte de dialogue "Attributs des méthodes" permet de modifier un attribut (Invisible, Disponible via Web Services etc.) pour tout ou partie des méthodes projet de la base de données en une seule opération. Cette fonction est très utile pour modifier les attributs d’un grand nombre de méthodes projet. Elle peut également être utilisée en cours de développement pour appliquer rapidement des attributs communs à des groupes homogènes de méthodes.

Pour modifier globalement les attributs des méthodes :

1. Dans la [Page Méthodes](https://doc.4d.com/4Dv20/4D/20.2/Methods-Page.300-6750119.en.html) de l'explorateur 4D, développez le menu des options, puis choisissez la commande **Modifier attributs globalement...**. La boîte de dialogue **Attributs des méthodes** apparaît.

2. Dans la zone “Méthodes à modifier”, saisissez une chaîne de caractères permettant de désigner les méthodes que vous souhaitez modifier globalement.
  La chaîne de caractères est utilisée comme critère de recherche des noms de méthodes.

Utilisez le caractère générique @ pour vous aider à définir des groupes de méthodes :

- pour désigner les méthodes dont le nom débute par..., saisissez @ en fin de chaîne. Par exemple : `web@`
- pour désigner les méthodes dont le nom contient..., saisissez @ en milieu de chaîne. Par exemple : `web@write`
- pour désigner les méthodes dont le nom se termine par..., saisissez @ en début de chaîne. Par exemple : `@write`
- Pour désigner toutes les méthodes, il suffit de taper @ dans la zone.

**Notes :**

- La recherche ne tient pas compte des majuscules et des minuscules.
- Vous pouvez saisir plusieurs caractères @ dans la chaîne, par exemple `dtro_@web@pro.@`

3. Dans la zone "Attribut à modifier", choisissez un attribut dans la liste déroulante puis cliquez sur le bouton radio **Vrai** ou **Faux** correspondant à la valeur à appliquer.

**Note :** Si l'attribut "Publié dans WSDL" est défini à Vrai, il ne sera appliqué qu'aux méthodes projet qui contiennent déjà l'attribut "Web Service".

4. Cliquez sur **Appliquer**. La modification est appliquée instantanément à toutes les méthodes projet désignées par la chaîne de caractères saisie.

