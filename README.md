CoursWebLp - GIT
==========

Vous trouverez ici un cours TP sur Git et ses utilisations.

# Partie 1 : utilisation d'un repository existant

Pour commencer nous allons découvrir ce que sont les commits et leur première utilité.

1. Tout d'abord allez sur github et forkez le repository de ce projet : https://github.com/NoobLad/CoursWebLp
 - Il vous faudra donc un compte github
 - Pour forker cliquez sur le bouton "fork" en haut à droite sur la page ci dessus. : ![alt text](https://raw.github.com/NoobLad/CoursWebLp/IMAGES/GIT/fork_button.png "Fork")
2. Placez vous dans un terminal avec git d'installé (Ici cloud9 sur un workspace indépendant de votre projet)
3. Puis faites : git clone {{url de votre fork}}
 - Pour l'url ce sera de ce genre là : https://github.com/{{nom d'utilisateur github}}/CoursWebLp.git
 - Ceci va faire une copie du repository en local dans un dossier nommé "CoursWebLp"
4. Placez vous dans le répertoire : cd CoursWebLp
5. Placez vous sur la branch "GIT" : git checkout GIT

# Partie 2 : un commit

Ici vous allez commencer à ajouter des fichiers, faire des modifications et les synchonizer avec le repos distant.

1. Faites un : git status
 - Vous devriez avoir un message précisant qu'il n'y a rien à commiter
2. Commencez par créer un fichier : touch entrainement
3. Puis refaites : git status
 - Vous devriez trouver votre fichier en rouge catégorisé dans les fichiers non suivis
4. Faites : git add entrainement
5. Puis : git status
 - votre fichier apparait dans la liste des changements à commiter
6. Maintenant il est temps de commiter : git commit -m"Voici un commentaire de commit"
 - Si vous faites un git status là votre fichier n'apparait plus : tous ses changements ont été enregistré.
7. Maintenant il va failloir envoyer vos modification au repos distant : git push origin GIT
 - "origin" correspond au nom attribué au repos distant par défaut lors du clone.
 - il est possible d'enregistrer plusieurs repos distant.
 - "GIT" correspond à la branch sur laquelle l'on pousse nos modifications. Il est possible de ne pas avoir les même nom des deux coté.
 - si vous vouler pousser sur origin et la même branche que celle sur laquelle vous travailler, les derniére versions de git permettent de faire simplement : git push
8. L'idée est la même pour la synchronisation dans le sens inverse, pour récupêrer les modifications distantes : git pull origin GIT
 - comme pour le précédent un raccourci existe : git pull

> Note : le principe est le même si le fichier existe déjà.
> Lister les commits : git log
> Lister les commits de façon un peu plus visuel : git log --pretty=format:"%h %s" --graph

# Partie 3 : Add all and ignore

Il est possible d'enregistrer toutes vos modification d'un seul coup, mais aussi de préciser ce qui ne doit pas être appartenir au versionning.
Il y a plusieurs situation oû l'on veut pouvoir ignorer un fichier, un exemple serais la version compilé d'une application.

1. Créez un fichier nommé ".gitignore"
 - Chaque ligne correspond a un pattern de fichier à ignorer. Example : *.class cela signifie que tout les fichiers dont l'extension est "class" seront ignoré.
2. Ajoutez y la ligne : justeUnTest
3. Puis créez un dossier nommé "justeUnTest" dans lequel vous ajouterez un fichier quelconque.
4. Faites : git status
 - Que constatez vous ?
5. Maintenant on commit mais un peu différemment de tout à l'heure : git commit -am"Add gitignore"
 - Vous vennez d'ajoutez tout les fichiers avecs des modifications en cours et de les commiter.
 - le "-a" est un raccourci qui produit le même effet que si vous aviez fait "git add ." qui ajoute au commit tout les fichiers avec des modification en cours.
6. Un petit git push pour finir

# Partie 4 : manipulation de commit

C'est mignon tout ça mais si j'ai fait une erreur ? Ba je vous souhaite que si cela arrive ce soit avant d'avoir poussé vos modifications sur le repos distant.
En général annulé un commit déjà synchronzé donne des résultats pas toujours génial. Mais si vous etes dans la situation oû tout se trouve en local faites comme suit :

1. Faites quelques commits sans les pousser.
2. Le premien moyen de revenir sur un commit est le "reset soft" qui permet de revenir en arrière sans perdre vos modification : git reset --soft HEAD~1
 - cela annulé le dernier commit sans perdre les changements. Si nous avions ecrit HEAD~2 nous aurions annulé les deux derniers, etc...
3. Le second moyen est : git reset --hard HEAD~1
 - Ici toutes les modifications apporté par le commit sont tout simplement jeté.

> Attention : Utilisez le reset hard avec vigilance !
> Une commande existe si vous ne pouvez pas complétement annulé un commit : git revert {{identifiant du commit}}

# Partie 5 : mettre de coté

Dans git existe le stash. C'est un endroit ou vous pouvez mettre de coté les modifications en cours.

1. Faites quelques modifications ci et là sans les commiter.
2. Faites : git stash
 - Vos modifications ont disparu. Elles sont dans le stash
3. Faites : git stash list
 - Vous verrez vos modification ici elle devrait se nommer {0}
4. Faites : git stash pop
 - Vos modifications sont revenu. Mais ne sont plus dans git stash list.
 - pop applique le dernies stash en fait, et le retire de la liste.
5. Faites : git stash save "monStash"
 - Vos modification apparaissent dans git stash list sous le nom de "monStash"
6. Faites : git stash apply "monStash"
 - Vous récupérez vos modifications mais elles ne sont pas supprime du stash
7. Faites : git stash drop "monStash"
 - Le stash est effacé.

# Partie 6 : manipulation de branche

Nous allons voir comment créer et fusionner des branches.

1. Pour créer une branche depuis celle oû vous vous trouvez : git checkout -b GITBranchTest
 - Cela cré une branche et vous bascule directement dessus.
 - C'est un raccourci pour : git branch GITBranchTest && git checkout GITBranchTest
2. Faites un : git branch
 - Permet de lister l'ensemble des branches existantes.
3. Faites quelques modifications et commitez les.
4. Revenez sur la branche GIT : git checkout GIT
5. Fusionnez les deux branches : git merge GITBranchTest
 - votre branche viens d'être fusionner
 - Pour constater : git branch
