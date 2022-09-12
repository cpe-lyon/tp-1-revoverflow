**Thomas POYETON - 3ICS**

# TP 2 - Bash

1. On retrouve les commandes tapées par l'utilisateur dans les dossiers spécifiés dans la variable d'environnement "PATH" en l'occurence :
- /usr/local/sbin
- /usr/local/bin
- /usr/sbin
- /usr/bin
- /sbin
- /bin
- /usr/games
- /usr/local/games
- /snap/bin

2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?

La variable d'environnement HOME permet de retourner dans le répertoire personnel.

3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL.

- LANG : permet de définir la langue du système
- PWD : permet de définir le répertoire courant
- OLDPWD : permet de définir le répertoire précédent
- SHELL : permet de définir le shell utilisé

4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.

```bash
$ MY_VAR="test"
$ echo $MY_VAR
test
```

5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.

La commande bash permet de lancer un nouveau shell bash. La variable MY_VAR n'existe plus car elle est locale.

6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.

```bash
$ export MY_VAR
$ bash
$ echo $MY_VAR
test
```

7. Créer la variable d’environnement NOM ayant pour contenu vos prénom et nom séparés par un espace. Afficher la valeur de NOM pour vérifier que l’affectation est correcte.

```bash
$ NOM="Thomas POYETON"
$ echo $NOM
Thomas POYETON
```

8. Ecrivez une commande qui affiche ”Bonjour à vous, prenom nom !” en utilisant la variable NOM

```bash
$ echo "Bonjour à vous, ${NOM} !"
Bonjour à vous, Thomas POYETON !
```

9. Quelle différence y a-t-il entre donner une valeur vide à une variable d’environnement et l’utilisation de la commande unset ?

La commande unset supprime la variable alors que la valeur vide ne supprime pas la variable.

10. . Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)

```bash
$ echo "\$HOME = $HOME"
$HOME = /home/User
```

## Exercice 2

Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher.

```bash
#!/bin/bash

PASSWORD="test"

read -s -p "Entrez le mot de passe : " password

if [ "$password" = "$PASSWORD" ]; then
    echo "Mot de passe correct"
else
    echo "Mot de passe incorrect"
fi
```

## Exercice 3

Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètre est un nombre réel :

```bash
#!/bin/bash

function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'

    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

if is_number $1; then
    echo "Le paramètre est un nombre"
else
    echo "Le paramètre n'est pas un nombre"
fi
```

## Exercice 4

Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement)

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "Utilisation : $0 nom_utilisateur"
    exit 1
fi

if id -u $1 >/dev/null 2>&1; then
    echo "L'utilisateur $1 existe"
else
    echo "L'utilisateur $1 n'existe pas"
fi
```

## Exercice 5

Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que l’utilisateur saisit toujours un entier naturel)

```bash
#!/bin/bash

function factorielle()
{
    if [ $1 -eq 0 ]; then
        echo 1
    else
        echo $(($1 * $(factorielle $(($1 - 1)))))
    fi
}

if [ $# -eq 0 ]; then
    echo "Utilisation : $0 nombre"
    exit 1
fi
```

## Exercice 6

Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner. Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).

```bash
#!/bin/bash

nombre=$(($RANDOM % 1000 + 1))
echo "Devinez le nombre entre 1 et 1000"

while true; do
    read -p "Entrez un nombre : " nombre_saisi

    if [ $nombre_saisi -eq $nombre ]; then
        echo "Gagné !"
        break
    elif [ $nombre_saisi -lt $nombre ]; then
        echo "C'est plus !"
    else
        echo "C'est moins !"
    fi
done
```

## Exercice 7


1. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres sont bien des entiers.


```bash
#!/bin/bash

function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'

    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

if [ $# -eq 0 ]; then
    echo "Utilisation : $0 nombre1 nombre2 nombre3"
    exit 1
fi

for i in $@; do
    if ! is_number $i; then
        echo "Erreur : $i n'est pas un nombre"
        exit 1
    fi
done

min=$1
max=$1

for i in $@; do
    if [ $i -lt $min ]; then
        min=$i
    fi

    if [ $i -gt $max ]; then
        max=$i
    fi
done

moyenne=$(($1 + $2 + $3))

echo "Min : $min"
echo "Max : $max"
echo "Moyenne : $moyenne"
```

2. Généralisez le programme à un nombre quelconque de paramètres (pensez à SHIFT)


```bash
#!/bin/bash

function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'

    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

if [ $# -eq 0 ]; then
    echo "Utilisation : $0 nombre1 nombre2 nombre3 ..."
    exit 1
fi

for i in $@; do
    if ! is_number $i; then
        echo "Erreur : $i n'est pas un nombre"
        exit 1
    fi
done

min=$1
max=$1

for i in $@; do
    if [ $i -lt $min ]; then
        min=$i
    fi

    if [ $i -gt $max ]; then
        max=$i
    fi
done

moyenne=0

for i in $@; do
    moyenne=$(($moyenne + $i))
done

echo "Min : $min"
echo "Max : $max"
echo "Moyenne : $moyenne"
```

3. Modifiez votre programme pour que les notes ne soient plus données en paramètres, mais saisies et stockées au fur et à mesure dans un tableau.

```bash
#!/bin/bash

function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'

    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}

notes=()

while true; do
    read -p "Entrez une note (q pour quitter) : " note

    if [ $note = "q" ]; then
        break
    fi

    if ! is_number $note; then
        echo "Erreur : $note n'est pas un nombre"
        exit 1
    fi

    notes+=($note)
done

min=${notes[0]}

for i in ${notes[@]}; do
    if [ $i -lt $min ]; then
        min=$i
    fi

    if [ $i -gt $max ]; then
        max=$i
    fi
done

moyenne=0

for i in ${notes[@]}; do
    moyenne=$(($moyenne + $i))
done

echo "Min : $min"
echo "Max : $max"
echo "Moyenne : $moyenne"
```

## Exercice 8

Écrivez un script qui affiche les combinaisons possibles de couleurs (cf. TP 1) :

```bash
#!/bin/bash

for i in $(seq 0 7); do
    for j in $(seq 0 7); do
        echo -e "\e[3${i};4${j}mCouleur de texte : $i, couleur de fond : $j\e[0m"
    done
done
```
