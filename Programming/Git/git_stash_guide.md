# Git Stash --- Guida Completa

## Cos'è git stash

`git stash` permette di salvare temporaneamente le modifiche non
commitate (working directory e staging area) per poter tornare a uno
stato pulito del repository.

È utile quando devi cambiare branch o fare un pull senza creare un
commit provvisorio.

------------------------------------------------------------------------

## Cosa salva stash

Per default salva:

-   Modifiche nella **Working Directory**
-   Modifiche nella **Staging Area (Index)**

Non salva i file non tracciati, a meno che non venga specificato.

------------------------------------------------------------------------

## Comandi principali

### Salvare le modifiche

``` bash
git stash
```

### Salvare includendo file non tracciati

``` bash
git stash -u
```

### Salvare con messaggio descrittivo

``` bash
git stash push -m "lavoro temporaneo su feature X"
```

------------------------------------------------------------------------

## Visualizzare gli stash

``` bash
git stash list
```

Ogni stash è identificato come:

    stash@{0}
    stash@{1}
    ...

------------------------------------------------------------------------

## Riapplicare uno stash

### Applicare l'ultimo stash

``` bash
git stash apply
```

### Applicare uno stash specifico

``` bash
git stash apply stash@{1}
```

### Applicare e rimuovere dallo stack

``` bash
git stash pop
```

------------------------------------------------------------------------

## Eliminare uno stash

``` bash
git stash drop stash@{0}
```

Eliminare tutti gli stash:

``` bash
git stash clear
```

------------------------------------------------------------------------

## Come funziona internamente

Quando esegui `git stash`, Git crea uno o più commit speciali che
vengono salvati in una struttura interna chiamata *stash stack*.

Non modifica la cronologia del branch corrente. È una soluzione
temporanea, non un sostituto dei commit.

------------------------------------------------------------------------

## Quando usare stash

-   Devi cambiare branch rapidamente
-   Devi fare pull ma hai modifiche locali
-   Vuoi testare qualcosa senza perdere il lavoro corrente

------------------------------------------------------------------------

## Flusso tipico

``` bash
git stash
git switch main
# lavoro urgente
git switch feature
git stash pop
```

Questo permette di sospendere temporaneamente il lavoro senza creare
commit non necessari.


---

## Navigazione

- [Indice Git](00_Index.md)
- [Indice Programming](../00_Index.md)
