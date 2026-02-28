---
owner: Daniele Andreis
created: November 14, 2025 – 19:43 AM
updated: 2025-11-14
tags: [git]
---


# Intro

È un sistema di versionamento **distribuito**. Perché usarlo:

- gestire il lavoro di un gruppo su uno stesso progetto (gestione conflitti etc).
- mantenere uno storico di un progetto.
- organizzare il progetto (branches).

Rispetto ad altri (CVS, subversion...) non lavora per "differenze" ma fa degli snapshot della situazione.

Git è un **database di oggetti indirizzati per hash**.

Ci sono 4 tipi principali di oggetti:

- **blob** → contenuto di un file
    
- **tree** → struttura delle cartelle
    
- **commit** → snapshot + metadata
    
- **tag** → etichette annotate



# Basi

I file possono essere in uno dei seguenti stati:

1. *committed* (salvato nel db)
2. *modified* (salvati solo nella working directory)
3. *staged* (salvati nella working directory e marcati per essere committati)

Per la configurazione (username, editor, colori....) ci sono 3 livelli:

1. globale (/etc/gitconfig o git config --system ....)
2. locale, a livello utente (/home/user/.gitconfig o git config --global)
3. locale, per progetto (./progetto/.git/config)

## Esempio di gestione dei branch

[[https://nvie.com/posts/a-successful-git-branching-model/]]

> Questo esempio illustra come organizzare i branch in fase di sviluppo.
> Posso anche creare branch per ogni personalizzazione del codice, se lo distribuisco a persone diverse.

![[git_branch.png]]

## Log

```
git log -p -2 #per vedere la diff
git log --stat
git shortlog #vede per utente
git reflog  #solo locale HEAD{@}
git log master..branch1 #vedo quello che c'è in branch1 e non in master
git log master...branch1 #commit in master e branch1 che non hanno niente in comune

```

Nota:

- `^N` indica il parent (esempio: `git show HEAD^`)
- `~N` indica la profondità nella storia

## Tag

- lightweight
- annotated => migliore: git tag -a

## Altri comandi

```
git rm --cached
git commit --amend #unisce commit o cambia commento
git stash push -m "commento"
$....

```

# Hooks

Sono in .git/hooks

### Client-side hooks

Gli script non sono clonati sono solo locali!!!! usati per fare i test etc...

- pre-committing hooks (verifiche, lint,trail space) [[https://bitbucket.org/centrometeo/wiki/src/e097d034c03c3ac2cbd2c04fc8826b3aa7cae5d6/git/pre-commit?at=master&fileviewer=file-view-default]]
- prepare-commit-msg (in commit autogenerati o con template-commit)
- commit-msg *verifica se il messaggio è corretto)
- post-commit

Altri hooks:

- pre-rebase
- post-checkout
- post-merge

### Server-side

- pre-received
- post-received
- update

# Migrazione

Ottenere informazioni su tutti i branch nel remoto

```
 git fetch origin

```

Controllare di avere in locale tutti i branch

```
git branch -a  (Controllare di avere in locale tutti i branch)

```

Crea il riferimento al nuovo repo:

```
git remote add nuovo_repo https:/....

```

Eseguire il push sul nuovo repository

```
 git push --all nuovo_repo

```

```
git push --tags nuovo_repo

```

Cancello il vecchio repo e rinomino il nuovo

```
git remote rm origin

```

```
git remote rename nuovo_repo origin

```

# Merge di repository

[[https://www.w3docs.com/snippets/git/how-to-merge-two-git-repositories.html]]

# Risorse

- [[https://gist.github.com/bubbobne/47017106854a862dec23d4c36dc3ae5c]]
- [[https://git-scm.com/book/en/v2]]
- [[https://martinfowler.com/articles/branching-patterns.html]]

---

## Navigazione

- [Indice Git](00_Index.md)
- [Indice Programming](../00_Index.md)
