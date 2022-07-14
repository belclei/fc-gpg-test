# Documentação do processo de geração de chave para assinatura de commits no github

## Instalação do cli do GPG

`brew install gpg`

## Verificar se já há uma chave gerada neste computador

Para a verificação deve-se executar o seguinte comando: `gpg --list-secret-key --keyid-form LONG`

Abaixo está o retorno caso já exista uma chave, sendo que, o id é `A0FDAB41637F650`:

```bash
------------------------------
sec   rsa4096/A0FDAB41637F650 2022-07-14 [SC] [expires: 2023-07-14]
      CCDB2A4B3A5E4C7720B3ACFA0FDAB41637EF650
uid                 [ultimate] belclei <belclei@gmail.com>
ssb   rsa4096/72A45E85F018EE3 2022-07-14 [E] [expires: 2023-07-14]
```

## Geração de uma chave GPG

No Exemplo abaixo,

- digitei o comando `gpg --full-generate-key`,
- selecionei `1` para gerar uma chave do tipo RSA,
- escolhi `4096` como tamanho em bits da chave,
- selecionei `1y` para a chave expirar em ano,
- e confirmei a geração da chave;
- Depois informei o nome e o e-mail que utilizei nas configurações locais do git.
  - pode-se descobrir isso via `git config --global -l`.
- E novamente confirmei que estavam todos os dados corretos.
- Ao final, uma senha deve ser informada para a chave que será gerada.

```bash
gpg --full-generate-key
gpg (GnuPG) 2.3.7; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Por favor selecione o tipo de chave desejado:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Opção? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
O tamanho de chave pedido é 4096 bits
Por favor especifique por quanto tempo a chave deve ser válida.
         0 = chave não expira
      <n>  = chave expira em n dias
      <n>w = chave expira em n semanas
      <n>m = chave expira em n meses
      <n>y = chave expira em n anos
A chave é valida por? (0) 1y
Key expires at Qui 13 Jul 21:53:57 2023 -03
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Nome completo: belclei
Endereço de correio eletrónico: belclei@gmail.com
Comentário:
Você selecionou este identificador de utilizador:
    "belclei <belclei@gmail.com>"

Mudar (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? O
Precisamos gerar muitos bytes aleatórios. É uma boa ideia realizar outra
actividade (escrever no teclado, mover o rato, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma hipótese maior de ganhar entropia suficiente.
Precisamos gerar muitos bytes aleatórios. É uma boa ideia realizar outra
actividade (escrever no teclado, mover o rato, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma hipótese maior de ganhar entropia suficiente.
gpg: directory '/Users/guri/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/Users/guri/.gnupg/openpgp-revocs.d/CCDB2A4B3A5E54C7720B3ACFA0FDAB4637EF650.rev'
chaves pública e privada criadas e assinadas.

pub   rsa4096 2022-07-14 [SC] [expires: 2023-07-14]
      CCDB2A4B3A5E54C7720B3CFA0FDAB41637EF650
uid                      belclei <belclei@gmail.com>
sub   rsa4096 2022-07-14 [E] [expires: 2023-07-14]
```

## Ver a chave completa

Utilizando o id da chave, no caso A0FDAB4137EF650, utilizei o seguinte comando `gpg --armor --export A0FDAB4137EF650`. A resposta, conforme abaixo, deve ser copiada, para informar ao github.

```bash
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
PalCMrJC
=535H
-----END PGP PUBLIC KEY BLOCK-----
```

## No GitHub

- Copiar a chave toda, e em seguida acessar as configurações de seu usuário no github: `github.com/settings/keys`

- Clicar em `New GPG Key`

- Colar a chave pública e adicionar.

Agora toda vez que subir um commit deste usuário no github, a chave pública será verificada e se bater, vai aparecer como verificado.

## Últimas configurações

### Configurar assinatura no arquivo de configurações do git

- Informar a key que foi gerada: `git config --global user.signingkey AFDAB637EF90650`
- Configurar para assinar todos os commits por padrão `git config --global commit.gpgsign true`
- Configurar para assinar todas as tags por padrão `git config --global tag.gpgsign true`

### Variáveis de ambiente

- Adicionar a seguinte linha às variáveis de ambiente: `export GPG_TTY=$(tty)`
- Adicionar arquivo `~/.gnupg/gpg.conf` contendo somente o seguinte conteúdo: `use-agent`.
- Habilitar o agente do GPG, para evitar ter que digitar a senha toda vez que fizer um commit: `gpgconf --launch gpg-agent`.

## Dica

Para forçar a assinatura de um commit, utilizar a diretiva `-S`, conforme: `git commit -S -m '...msg...'`
