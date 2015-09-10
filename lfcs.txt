tmux
====

tmux.conf
---------
 unbind C-b
 set -g prefix C-a
 bind C-a send-prefix

Splitten
--------
C-a % : Vertikal
C-a " : horizontal
C-a x : schliesst
C-a cursor hÃ¼pft
C-a blank : cycled durch die verschiedenen layouts

 


vi
==
syntax on
set number
set background=dark

CTRL-V : Visual Column-Mode 
v : Visual Mode
Shift-V : Visual Line-Mode

anschliessend kann man mit Shift i inserten oder mit Shift a appenden. Wenn man dann ESC drÃckt, wird das auf alle Spalten angewandt

Tabs und Spaces mit
set listchars=tab:>_
set list


Shell
=====
echo $SHELL   
/etc/passwd    




root
====
sudo -i


Gruppen
=======
groupadd generiert neue Gruppe
useradd generiert neuen user
usermod modifiziert user, kann also z.B. GruppenzugehÃ¶rigkeit Ã¤ndern

File-Infos
==========
find 
locate
type : zeigt was es fÃr eine Art AUfruf ist! Zeigt zum Beispiel aliase an
which : zeigt an, welches command genutzt wird ( bei mehreren ) 
whereis : zeigt auch wie which das Binary an, zeigt aber auch an, wo die Manuals liegen


awk
===
Syntax : awk '{ print $2 }' file.txt


cut
===
-f 1-2 : Felder, separiert durch Tab
-c 3-6 : Characters 


column
======
-t macht pretty
Der Rest ist mir noch nicht ganz klar
column macht aus Zeilen eine Tabelle
die Breite der Tabelle laesst sich mit -c Characters festlegen 
echo "1 3 4 5 6 7 8 9 0"  | tr ' ' '\n' | column -c 30 


fdisk
=====
Blocksize kann man angeben, oder +Blocksize oder +GrÃsse
hier wird die Swap-Partition angelegt
Dann muss man noch  /etc/fstab die Swap-partiton anlegen (mountpoiunt none, type swap, sw)
und anschliessend noch swapon device benutzen

sed
===
Standard : sed -e 's/xxx/yyy/g' file
Da kann man sich das -e sparen
sed kann bestimmte Dinge nur auf Teile anwenden, zum Beispiel auf betsimmte Zeilen
sed -n xxx,yyyp file gibt file zwischen Zeile xxx und yyy aus, also sed -n 1,5p file ist
Ã¤quivalent zu head -5 file, aber zu sed -n 2,5p file gibts schon nix mehr...
  

tr
==
tr 'c1' 'c2' ersetzt c1 durch c2
tr -s 'c1'  ersetzt wiederholtes Vorkommen von c1 durch ein c1 
=> tr -s ' ' ersetzt Spaces durch ein Space!


LVM
===
Step 1 : pvcreate
Step 2 : pvscan
Step 3 : vgcreate
Step 4 : vgscan
Step 5 : lvcreate
Step 6 : lvscan
Step 7 : mkfs.ext
Step 8 : vi /etc/fstab

/etc/security/limits.d
======================
- Anazhl logins begrenzen, wirkt nur auf Login Shells, Examples selbsterklaerend


TODO
====

