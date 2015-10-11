tmux
====

tmux.conf
---------
 unbind C-b
 set -g prefix C-a
 bind C-a send-prefix

Splitten
--------
- C-a % : Vertikal  
- C-a " : horizontal  
- C-a x : schliesst  
- C-a cursor huepft  
- C-a blank : cycled durch die verschiedenen layouts   
- C-a Z zoomt ein und aus



vi
==
syntax on  
set number  
set background=dark  

CTRL-V : Visual Column-Mode   
v : Visual Mode  
Shift-V : Visual Line-Mode  

anschliessend kann man mit Shift i inserten oder mit Shift a appenden. Wenn man dann ESC drueckt, wird das auf alle Spalten angewandt  

Tabs und Spaces mit
set listchars=tab:>_,eol:¶
set list
Das umgekehrte P oben bekommt man mit CTRL-K PI.
Das ist ein digraph.
Alle digraphs bekommt man mit :digraphs

Shell
=====
- echo $SHELL   
- /etc/passwd    




root
====
sudo -i


Gruppen
=======

- groupadd generiert neue Gruppe
- useradd generiert neuen user
- usermod modifiziert user, kann also z.B. Gruppenzugehoerigkeit aendern

File-Infos
==========
- find 
- locate
- type : zeigt was es fuer eine Art AUfruf ist! Zeigt zum Beispiel aliase an
- which : zeigt an, welches command genutzt wird ( bei mehreren ) 
- whereis : zeigt auch wie which das Binary an, zeigt aber auch an, wo die Manuals liegen


awk
===
Syntax : awk '{ print $2 }' file.txt


cut
===
-f 1-2 : Felder, separiert durch Tab
-c 3-6 : Characters 


cat
===
- cat -T stellt Tabs dar!
- Als Vorbereitung wenn gecuted werden soll  

column
======
-t macht pretty
Der Rest ist mir noch nicht ganz klar
column macht aus Zeilen eine Tabelle
die Breite der Tabelle laesst sich mit -c Characters festlegen 
echo "1 3 4 5 6 7 8 9 0"  | tr ' ' '\n' | column -c 30 


fdisk
=====
- Blocksize kann man angeben, oder +Blocksize oder +Groesse
- hier wird die Swap-Partition angelegt
- Dann muss man noch  /etc/fstab die Swap-partiton anlegen (mountpoiunt none, type swap, sw)
- und anschliessend noch swapon device benutzen

sed
===
Standard : sed -e 's/xxx/yyy/g' file  
Da kann man sich das -e sparen  
sed kann bestimmte Dinge nur auf Teile anwenden, zum Beispiel auf betsimmte Zeilen  
sed -n xxx,yyyp file gibt file zwischen Zeile xxx und yyy aus, also sed -n 1,5p file ist  
Aequivalent zu head -5 file, aber zu sed -n 2,5p file gibts schon nix mehr...  
  

tr
==
tr 'c1' 'c2' ersetzt c1 durch c2
tr -s 'c1'  ersetzt wiederholtes Vorkommen von c1 durch ein c1 
=> tr -s ' ' ersetzt Spaces durch ein Space!


LVM
===
Step 1 : pvcreate /dev/sdb1 /dev/sdb2 ...
Step 2 : pvscan
Step 3 : vgcreate MeinVolume /dev/sdb1  /dev/sdb2 ...
Step 4 : vgscan
Step 5 : lvcreate --size xxx --name "yyy" MeinVolume
Step 6 : lvscan
Step 7 : mkfs.ext /dev/MeinVolume/yyy
Step 8 : vi /etc/fstab


/etc/security/limits.d
======================
- Anazhl logins begrenzen, wirkt nur auf Login Shells, Examples selbsterklaerend


FOR-Loops
=========
for i in {1..}; do echo "Hallo $i" ; echo "==========" ; echo " "; done



tar
===
tar -a detektiert den Kompressions-Algorithmus anhand der Extension

Things to remember or check
===========================
- Backups : tar -caf
- User processes : ps, top , kill
- Restoring : tar, permissions check
- File-permissions : ulimits
- Permissions : /etc/security/limits.d (pam)
- Accessing root account : /etc/sudoers
- Editing text on the command-line : cut, cat, sed, tac, tr, ...
- format filesystemss: mkfs.xxx, e2label,
- swap : mkswap
- Partitioning : fdsik
- LVM : pvcreate, vgcreate, lvcreate



TODO
====
for-Loops


