
# Git — Undoing Things (Summary)

## I tre livelli di Git

- **Working Directory** → file sul disco  
- **Staging Area (Index)** → cosa andrà nel prossimo commit  
- **Commit (HEAD)** → cronologia dei commit  

Ogni comando agisce su uno o più di questi livelli.

---

## Ripristinare modifiche locali

### Ripristinare file
```bash
git restore file.txt
```
Ripristina il file dall’ultimo commit (modifica solo la working directory).

### Togliere file dallo staging
```bash
git restore --staged file.txt
```
Rimuove il file dall’index ma mantiene le modifiche nella working directory.

`restore` non modifica la storia dei commit.

---

## Cambiare branch

```bash
git switch branch-name
```

`switch` è il comando moderno per cambiare branch.  
Sostituisce l’uso di `checkout` per questo scopo.

---

## Modificare l’ultimo commit

### Cambiare il messaggio
```bash
git commit --amend
```

### Aggiungere file dimenticati
```bash
git add file.txt
git commit --amend
```

`--amend` crea un nuovo commit (nuovo hash) che sostituisce l’ultimo.  
Non usarlo su commit già pushati su branch condivisi.

---

## Riscrivere la storia: reset

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

Modalità:

- `--soft` → sposta HEAD, mantiene staging e working directory  
- `--mixed` (default) → sposta HEAD, resetta staging  
- `--hard` → resetta commit, staging e working directory  

`reset` modifica la storia locale.

---

## Annullare un commit pubblicato

```bash
git revert <commit>
```

Crea un nuovo commit che annulla le modifiche del commit indicato.  
Non riscrive la storia ed è sicuro per branch condivisi.
