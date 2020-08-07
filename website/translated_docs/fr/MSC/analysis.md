---
id: analysis
title: Activity analysis Page
sidebar_label: Activity analysis Page
---

The Activity analysis page allows viewing the contents of the current log file. This function is useful for parsing the use of a database or detecting the operation(s) that caused errors or malfunctions. In the case of a database in client-server mode, it allows verifying operations performed by each client machine.
> It is also possible to rollback the operations carried out on the data of the database. For more information, refer to [Rollback page](rollback.md).

![](assets/en/MSC/MSC_analysis.png)

Every operation recorded in the log file appears as a row. The columns provide various information on the operation. You can reorganize the columns as desired by clicking on their headers.

This information allows you to identify the source and context of each operation:

- **Opération** : numéro de séquence de l’opération dans le fichier d’historique.
- **Action** : type d’opération effectuée. This column can contain one of the following operations:
    - Opening of Data File: Opening of a data file.
    - Closing of Data File: Closing of an open data file.
    - Creation of a Context: Creation of a process that specifies an execution context.
    - Closing of a Context: Closing of process.
    - Addition: Creation and storage of a record.
    - Adding a BLOB: Storage of a BLOB in a BLOB field.
    - Deletion: Deletion of a record.
    - Modification: Modification of a record.
    - Start of Transaction: Transaction started.
    - Validation of Transaction: Transaction validated.
    - Cancellation of Transaction: Transaction cancelled.
    - Update context: Change in extra data (e.g. a call to `CHANGE CURRENT USER` or `SET USER ALIAS`).

- **Table** : table à laquelle appartient l’enregistrement ajouté/supprimé/modifié ou le BLOB.
- **Clé primaire/BLOB** : contenu de la clé primaire de l'enregistrement (lorsque la clé primaire est composée de plusieurs champs, les valeurs sont séparées par des points-virgules), ou numéro de séquence du BLOB impliqué dans l’opération.
- **Process** : numéro interne du process dans lequel l’opération a été effectuée. Ce numéro interne correspond au contexte de l’opération. This internal number corresponds to the context of the operation.
- **Taille** : taille (en octets) des données traitées par l’opération.
- **Date et Heure** : date et heure à laquelle l’opération a été effectuée.
- **System User**: System name of the user that performed the operation. In client-server mode, the name of the client-side machine is displayed; in single-user mode, the session name of the user is displayed.
- **4D User**: 4D user name of the user that performed the operation. If an alias is defined for the user, the alias is displayed instead of the 4D user name.
- **Valeurs** : valeurs des champs de l’enregistrement en cas d’ajout ou de modification. The values are separated by “;”. Seules les valeurs représentables sous forme alphanumérique sont affichées.  
  ***Note** : Si la base est chiffrée et si aucune clé de données valide correspondant au fichier d'historique n'a été fournie, les valeurs chiffrées ne sont pas affichées dans cette colonne.*
- **Enregistrements** : Numéro de l’enregistrement.

Cliquez sur le bouton **Analyser** pour mettre à jour le contenu du fichier d’historique courant de la base sélectionnée (nommé par défaut nomdonnées.journal). The Browse button can be used to select and open another log file for the database. Le bouton **Exporter...** vous permet d’exporter le contenu du fichier sous forme de texte.


