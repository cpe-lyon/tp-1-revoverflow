Thomas POYETON
# TP n°1
## Exercice 2

Manuel
1. La commande which permet de localiser l’exécutable d’une
commande
2. On peut rechercher un terme dans le manuel grâce à “/terme”
3. Pour quitter le manuel il suffit de cliquer sur “q”
4. Il n’y a pas de 6ème section pour la page man de which
Navigation dans l’arborescence des fichiers
1.cd /var/log
2.cd .
3.cd
4.cd -
5. Nous n’avons pas la permission
6. Cela fonctionne car on a exécuté la commande en tant que
root (sudo)
7. mkdir Dossier1 Dossier2 Dossier2/Dossier2.1
Dossier2/Dossier2.2
touch Dossier1/Fichier1 Dossier2/Dossier2.2/Fichier2
Dossier2/Dossier2.2/Fichier3
8. Fichier1 est supprimé mais pas Dossier1
9. On utilise rm -d
10. On ne peut pas le supprimer car le dossier n’est pas vide
11.On utilise rm -rf Dossier2
Commandes importantes
1. La commande permettant d’afficher l’heure est “date” et “time”
permet de chronométrer l'exécution d’un programme.
Thomas POYETON
2. Les fichiers et dossiers commençant par un point sont cachés.
3./bin/ls
4. “ll” équivaut à “ls -alF”
5.ls /usr/bin
6. Elle liste les fichiers et dossiers du dossier parent au dossier
courant
7.pwd
8. Le contenu du fichier plop est remplacé par “bip”
9. La commande ajoute “bip” au fichier
10. “toto” est affiché et l'exécution dure 10 millisecondes
11.“file” permet de voir de quel format est un fichier
12. Les modification effectuées à “original” sont synchronisées
avec “lien_phy” et lorsque “original” est supprimé, “lien_phy”
garde le contenu du fichier ”original”.
13. Les modifications effectuées sur les deux fichiers sont
synchronisées dans les deux sens et lorsque le fichier
“lien_phy” est supprimé, le lien “lien_sym” n’est plus
fonctionnel (fichier introuvable)
14. tail -f /var/log/syslog
CTRL+C pour stopper le défilement
15. cat /var/log/syslog | head -n 5
cat /var/log/syslog | tail -n 15
cat /var/log/syslog | tail -n +10 | head -n 10
16. Cela affiche les logs systèmes dans un lecteur de fichier
interactif
17.Il contient les différents comptes utilisateurs présent sur la
machine. Pour le manuel du fichier : “man 5 passwd”
18. cut -d: -f1 /etc/passwd | sort -r
19. cat /etc/passwd | wc -l
20. man -k conversion | wc -l
21. find / -name passwd
22. find / -name passwd 2>/dev/null >
~/list_passwd_files.txt
23. grep “alias ll=” -r ~
Thomas POYETON
Il se trouve dans “~/.bashrc”
24. Impossible d’installer locate (problème réseau)
25. Impossible d’installer locate (problème réseau)
## Exercice 3
1. cp /var/log/syslog ~/log.txt
nano ~/log.txt
2. On utilise Ctrl + \ puis “A” pour tout remplacer
3. On déplace avec Ctrl + K et Ctrl + U les premières lignes vers le bas
4. On annule avec Alt + U
5. Et on quitte avec Ctrl + S et Ctrl + X
## Exercice 4
1. cp ~/.bashrc ~/.bashrc_bak
2. nano .bashrc
3. Les couleurs apparaissent
4. 
```bash
export PS1="\[\033[38;5;197m\][\@]\[$(tput sgr0)\] \[$(tput sgr0)\]\[\033[38;5;16m\]-\[$(tput sgr0)\] \[$(tput sgr0)\] [\033[38;5;119m\]\u@\[$(tput sgr0)\]\[\033[38;5;120m\]\H\[$(tput sgr0)\]\[\033[38;5;16m\]:\[$(tput sgr0)\]\[\033[38;5;14m\]\w\[$(tput sgr0)\]\[\033[38;5;16m\]\\$\[$(tput sgr0)\]"
```