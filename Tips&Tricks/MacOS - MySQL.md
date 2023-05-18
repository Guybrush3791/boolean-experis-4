## [opzionale] Install Homebrew 
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## [opzionale] Remove MAMP
Disinstallare MAMP attraverso il gestore di applicazioni

## Installare MySQL server
```sh
brew install mysql
```

## Settare la password di root
```sh
mysql_secure_installation
```

Verranno fatte diverse domande. Rispondere **NO** alla prima (`security policy`), dare la password di `root` desiderata e rispondere **YES** a tutto il resto

## Verifica
```sh
mysql -u root -p
```

Dando la password inserita in fase di installazione, si ottiene il seguente output:
```sh
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 6
Server version: 10.11.2-MariaDB Arch Linux

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```