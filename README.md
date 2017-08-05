# Hallsonware

Written in JScript (No. This is not JavaScript).

#### Português

Uma chave é gerada aleatóriamente (`Music.mp3.key`) e cifrada (`Music.mp3.key.enc`) através da chave pública auto-contida no `Document.docx.js`.

A chave decifrada é usada para cifrar o arquivo alvo (`Music.mp3`), dando origem ao arquivo alvo cifrado (`Music.mp3.enc`).

O arquivo alvo decifrado e a chave decifrada são excluídos.

A chave cifrada é anexada ao arquivo cifrado (últimos 256 bytes).

Somente com a chave privada `private.pem` é possível recuperar o arquivo alvo decifrado.

Dessa forma, cada arquivo pode ser decifrado individualmente.

#### English

A key is generated randomly (`Music.mp3.key`) and encrypted (`Music.mp3.key.enc`) through the self-contained public key in `Document.docx.js`.

The decrypted key is used to encrypt the target file (`Music.mp3`), giving rise to the encrypted target file (`Music.mp3.enc`).

The decrypted target file and the decrypted key are deleted.

The encrypted key is appended to the encrypted file (last 256 bytes).

Only with the `private.pem` private key is it possible to recover the decrypted target file.

In this way, each file can be decrypted individually.

## Usage

1. Configure `targetFolders` and `targetExtensions` in the `Document.docx.js`.

2. Double-click on `Document.docx.js`.

## Todo

- [ ] Add Gutmann method [https://en.wikipedia.org/wiki/Gutmann_method](https://en.wikipedia.org/wiki/Gutmann_method)
