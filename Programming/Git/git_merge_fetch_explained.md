# Git Merge, Fast-Forward, Three-Way Merge, Fetch, Remotes, Rebase e Mergetool

------------------------------------------------------------------------

# Merge

## Commit con genitori multipli (merge commit)

Normalmente un commit ha **un solo genitore**.

Quando unisci due branch con storie divergenti, Git crea un **merge
commit** con **due (o più) genitori**:

-   il commit su cui ti trovi
-   il commit del branch che stai unendo

Questo commit rappresenta il punto di ricongiungimento delle due linee
di sviluppo.

------------------------------------------------------------------------

## Fast-Forward Merge

Un *fast-forward* avviene quando il branch che stai unendo è
semplicemente più avanti rispetto al commit corrente.

Esempio:

C1 --- C2 (main)\
C3 --- C4 (hotfix)

Se sei su C2 e fai merge di hotfix, Git non crea un nuovo commit. Sposta
semplicemente il puntatore di main a C4.

Nessun merge commit viene creato.

------------------------------------------------------------------------

## Merge con divergenza (Three-Way Merge)

Se la storia è così:

        C3 — C4 (feature)
       /

C1 --- C2\
C5 --- C6 (main)

Qui i branch hanno divergiuto dopo C2.

Git esegue un **three-way merge** usando:

1.  Il commit corrente (C6)
2.  Il commit del branch da unire (C4)
3.  Il loro antenato comune (C2)

Viene creato un nuovo merge commit con due genitori.

------------------------------------------------------------------------

# Rebase

## Cos'è rebase

`git rebase` riscrive la storia spostando una sequenza di commit su una
nuova base.

Invece di creare un merge commit, rebase:

-   prende i tuoi commit
-   li "riapplica" sopra un altro commit
-   crea nuovi commit con nuovi hash

Esempio:

Situazione iniziale:

        C3 — C4 (feature)
       /

C1 --- C2\
C5 --- C6 (main)

Con:

git rebase main

Git fa:

1.  Trova l'antenato comune (C2)
2.  Prende C3 e C4
3.  Li riapplica sopra C6

Risultato:

C1 --- C2 --- C5 --- C6 --- C3' --- C4'

La storia diventa lineare.

------------------------------------------------------------------------

## Differenza Merge vs Rebase

Merge: - Mantiene la struttura reale dei branch - Crea un commit con
genitori multipli

Rebase: - Riscrive la storia - Produce una cronologia lineare - Crea
nuovi commit (hash diversi)

------------------------------------------------------------------------

## Quando usare rebase

✔ Per aggiornare una feature branch locale prima di fare merge\
✔ Per mantenere una storia più pulita e lineare\
✔ Prima di aprire una pull request (se lavori da solo sulla branch)

------------------------------------------------------------------------

## Quando NON usare rebase

✘ Su branch già condivisi con altre persone\
✘ Su branch già pushati e usati da altri\
✘ Se non sei sicuro delle conseguenze sulla cronologia

Perché?

Rebase cambia gli hash dei commit. Se altri hanno già lavorato su quei
commit, si crea confusione e conflitti difficili da risolvere.

------------------------------------------------------------------------

# git mergetool

Quando Git non riesce a risolvere automaticamente un conflitto:

git mergetool

Apre uno strumento grafico per risolvere manualmente i conflitti.

------------------------------------------------------------------------

# git fetch

git fetch origin

Scarica nuovi commit dal remoto ma **non modifica il tuo branch
locale**.

Aggiorna solo i remote-tracking branch (es: origin/main).

------------------------------------------------------------------------

# Remotes

## Cos'è un remote

Un remote è un collegamento a un repository esterno (GitHub, GitLab,
server, ecc.).

Il nome più comune è:

origin

------------------------------------------------------------------------

## Comandi principali

Vedere i remote:

git remote -v

Push:

git push origin main

Pull:

git pull origin main

Pull equivale a:

git fetch origin git merge origin/main

------------------------------------------------------------------------

# Riassunto concettuale

-   Fast-forward → sposta il puntatore\
-   Merge → crea commit con genitori multipli\
-   Rebase → riscrive la storia rendendola lineare\
-   Fetch → aggiorna informazioni dal remoto\
-   Push → invia commit al server\
-   Remote-tracking branch → fotografia dello stato remoto
