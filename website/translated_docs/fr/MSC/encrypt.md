---
id: encrypt
title: Encrypt Page
sidebar_label: Encrypt Page
---

Vous pouvez vous aider de cette page pour chiffrer ou *déchiffrer* (i.e. enlever le chiffrement) le fichier de données, en fonction du statut de l'attribut **Chiffrable** défini pour chaque table de la base. For detailed information about data encryption in 4D, please refer to the "Encrypting data" section.

A new folder is created each time you perform an encryption/decryption operation. Il est nommé "Replaced Files (Encrypting) *yyyy-mm-dd hh-mm-ss*" ou "Replaced Files (Decrypting) *yyyy-mm-dd hh-mm-ss*".
> Encryption is only available in [maintenance mode](overview.md#display-in-maintenance-mode). If you attempt to carry out this operation in standard mode, a warning dialog will inform you that the database will be closed and restarted in maintenance mode

**Warning:**
- Encrypting a database is a lengthy operation. It displays a progress indicator (which could be interrupted by the user). Note also that a database encryption operation always includes a compacting step.
- Each encryption operation produces a copy of the data file, which increases the size of the application folder. It is important to take this into account (especially in macOS where 4D applications appear as packages) so that the size of the application does not increase excessively. Manually moving or removing the copies of the original file inside the package can be useful in order to minimize the package size.

## Encrypting data for the first time
Encrypting your data for the first time using the MSC requires the following steps:

1. Dans l'éditeur de structure, cochez l'attribut **Chiffrable** pour chaque table dont vous souhaitez chiffrer les données. See the "Table properties" section.
2. Open the Encrypt page of the MSC. Si vous ouvrez la page sans paramétrer les tables comme étant **Chiffrables**, le message suivant s'affiche : ![](assets/en/MSC/MSC_encrypt1.png) Sinon, le message suivant s'affiche : ![](assets/en/MSC/MSC_encrypt2.png) Cela signifie que le statut **Chiffrable** défini pour au moins une table a été modifié et que le fichier de données n'a toujours pas été chiffré. **Note : **Le même message s'affiche lorsque le statut **Chiffrable** a été modifié dans un fichier de données déjà chiffré ou après le déchiffrement d'un fichier de données (voir ci-dessous).
3. Cliquez sur le bouton de Chiffrement.  
   ![](assets/en/MSC/MSC_encrypt3.png)  
   Vous serez ensuite invité à saisir une phrase secrète pour votre fichier de données : ![](assets/fr/MSC/MSC_encrypt4.png) La phrase secrète est utilisée pour générer la clé de chiffrement des données. A passphrase is a more secure version of a password and can contain a large number of characters. For example, you could enter a passphrases such as "We all came out to Montreux" or "My 1st Great Passphrase!!" The security level indicator can help you evaluate the strength of your passphrase: ![](assets/en/MSC/MSC_encrypt5.png) (deep green is the highest level)
4. Enter to confirm your secured passphrase.

The encrypting process is then launched. If the MSC was opened in standard mode, the database is reopened in maintenance mode.

4D offers to save the encryption key (see [Saving the encryption key](#saving-the-encryption-key) below). You can do it at this moment or later. You can also open the encryption log file.

If the encryption process is successful, the Encrypt page displays Encryption maintenance operations buttons.

**Attention :** Durant l'opération de chiffrement, 4D créé un nouveau fichier de données vide et y insère des données à partir du fichier de données original. Records belonging to "encryptable" tables are encrypted then copied, other records are only copied (a compacting operation is also executed). If the operation is successful, the original data file is moved to a "Replaced Files (Encrypting)" folder. If you intend to deliver an encrypted data file, make sure to move/remove any unencrypted data file from the database folder beforehand.

## Encryption maintenance operations
When a database is encrypted (see above), the Encrypt page provides several encryption maintenance operations, corresponding to standard scenarios. ![](assets/en/MSC/MSC_encrypt6.png)


### Providing the current data encryption key
For security reasons, all encryption maintenance operations require that the current data encryption key be provided.

- If the data encryption key is already loaded in the 4D keychain(1), it is automatically reused by 4D.
- If the data encryption key is not found, you must provide it. The following dialog is displayed: ![](assets/en/MSC/MSC_encrypt7.png)

At this step, you have two options:
- entrer la phrase secrète actuelle(2) et cliquer sur **OK**. OU
- connecter un appareil tel qu'une clé USB et cliquer sur le bouton **Scanner les disques**.

(1) Le trousseau de 4D stocke toutes les clés de chiffrement de données valides saisies durant la session d'application session.   
(2) Le mot de passe actuel correspond au mot de passe utilisé pour générer la clé de chiffrement actuelle.

In all cases, if valid information is provided, 4D restarts in maintenance mode (if not already the case) and executes the operation.

### Re-encrypt data with the current encryption key

Cette opération est utile lorsque l'attribut **Chiffrable** a été modifié pour une ou plusieurs tables contenant des données. In this case, to prevent inconsistencies in the data file, 4D disallows any write access to the records of the tables in the application. Re-encrypting data is then necessary to restore a valid encryption status.

1. Cliquez sur **Re-chiffrer les données à l'aide de la clé actuelle**.
2. Enter the current data encryption key.

The data file is properly re-encrypted with the current key and a confirmation message is displayed: ![](assets/en/MSC/MSC_encrypt8.png)

### Change your passphrase and re-encrypt data
This operation is useful when you need to change the current encryption data key. For example, you may need to do so to comply with security rules (such as requiring changing the passphrase every three months).

1. Cliquez sur **Changer votre phrase secrète et re-chiffrer les données**.
2. Enter the current data encryption key.
3. Enter the new passphrase (for added security, you are prompted to enter it twice): ![](assets/en/MSC/MSC_encrypt9.png) The data file is encrypted with the new key and the confirmation message is displayed. ![](assets/en/MSC/MSC_encrypt8.png)

### Decrypt all data
This operation removes all encryption from the data file. If you no longer want to have your data encrypted:

1. Cliquez sur **Enlever le chiffrement de toutes les données**.
2. Enter the current data encryption key (see Providing the current data encryption key).

The data file is fully decrypted and a confirmation message is displayed: ![](assets/en/MSC/MSC_encrypt10.png)
> Once the data file is decrypted, the encryption status of tables do not match their Encryptable attributes. Pour restituer un statut de mise en correspondance, vous devez décocher tous les attributs **Chiffrable** au niveau de la structure de la base.

## Saving the encryption key

4D allows you to save the data encryption key in a dedicated file. Storing this file on an external device such a USB key will facilitate the use of an encrypted database, since the user would only need to connect the device to provide the key before opening the database in order to access encrypted data.

You can save the encryption key each time a new passphrase has been provided:

- when the database is encrypted for the first time,
- when the database is re-encrypted with a new passphrase.

Successive encryption keys can be stored on the same device.

## Log file
After an encryption operation has been completed, 4D generates a file in the Logs folder of the database. Il est créé au format XML et nommé "*DatabaseName_Encrypt_Log_yyyy-mm-dd hh-mm-ss.xml*" ou "*DatabaseName_Decrypt_Log_yyyy-mm-dd hh-mm-ss>.xml*".

An Open log file button is displayed on the MSC page each time a new log file has been generated.

The log file lists all internal operations executed pertaining to the encryption/decryption process, as well as errors (if any).
