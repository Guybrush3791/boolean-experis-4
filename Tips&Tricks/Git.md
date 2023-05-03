# Creazione nuovo progetto
*Dopo essere entrato in cartella progetto* da terminale, do i seguenti comandi:
```sh
git init                                                                        git add -A
git commit -m "init commit"
git branch -M main
# copiare questa riga dalla pagina della repo di GitHub
# git remote add origin git@github.com:Guybrush3791/test.git
git push -u origin main 
```

# Caricare modifiche progetto esistente
*Dopo essere entrato in cartella progetto* da terminale, do i seguenti comandi:
```sh
git add -A
git commit -m "new update super fix"
git push
```

# Scaricare modifiche progetto esistente
*Dopo essere entrato in cartella progetto* da terminale, do i seguenti comandi:
```sh
git pull
```

> [!attention] SOLO PER DOCUMENTAZIONE
> Utilizzare il seguente comando per annullare tutte le modifiche locali e scaricare la versione piu' aggiornata:
> ```
> git stash
> ```

