# LFCS

## Jogis Things to Remember , Todos etc for the LFCS

tmux
====

tmux.conf
---------
    unbind C-b  
    set -g prefix C-a  
    bind C-a send-prefix  
    
As I still can't remember these I usually do: `man tmux | tail -30 >> ~/.tmux.conf` because it is one of the last examples in tmux-manpage. You then just can edit .tmux.con ...


Splitten
--------
    C-a % : Vertikal  
    C-a " : horizontal    
    C-a x : schliesst   
    C-a cursor huepft    
    C-a blank : cycled durch die verschiedenen layouts   
    C-a Z zoomt ein und aus  



vi
==
    syntax on  
    set number  
    set background=dark  

CTRL-V : Visual Column-Mode     
v : Visual Mode  
Shift-V : Visual Line-Mode  

anschliessend kann man mit Shift i inserten oder mit   
Shift a appenden.   
Wenn man dann ESC drueckt, wird das auf alle Spalten angewandt  

Tabs und Spaces mit

    set listchars=tab:>_,eol:¶  
    set list  

Das umgekehrte P oben bekommt man mit CTRL-K PI.  
Das ist ein digraph.   
Alle digraphs bekommt man mit :digraphs  

Shell
=====
* echo $SHELL   
* /etc/passwd    


root
====
    sudo -i  


Gruppen
=======

* groupadd generiert neue Gruppe
* useradd generiert neuen user
* usermod modifiziert user, kann also z.B. Gruppenzugehoerigkeit aendern

File-Infos
==========

* find 
* locate
* type : zeigt was es fuer eine Art Aufruf ist! Zeigt zum Beispiel aliase an
* which : zeigt an, welches command genutzt wird ( bei mehreren ) 
* whereis : zeigt auch wie which das Binary an, zeigt aber auch an, wo die Manuals liegen


awk
===

    Syntax : awk '{ print $2 }' file.txt


cut
===

    -f 1-2 : Felder, separiert durch Tab  
    -c 3-6 : Characters  


cat
===

    _cat -T file_ stellt Tabs von file dar!
    Als Vorbereitung wenn gecuted werden soll  

head und tail
=============

* _head -xxx file_gibt xxx Zeilen vom Anfang von file aus
* _tail -n +xxx file_ schneidet xxx Zeilen vom Anfang von file ab !
* _tail -xxx file_ gibt die letzten xxx Zeilen des Endes von file aus


column
======

-t macht pretty    
Der Rest ist mir noch nicht ganz klar    
column macht aus Zeilen eine Tabelle    
die Breite der Tabelle laesst sich mit -c Characters festlegen     
echo "1 3 4 5 6 7 8 9 0"  | tr ' ' '\n' | column -c 30    


fdisk
=====

* Blocksize kann man angeben, oder +Blocksize oder +Groesse
* hier wird die Swap-Partition angelegt
* Dann muss man noch  /etc/fstab die Swap-partiton anlegen (mountpoiunt none, type swap, sw)
* und anschliessend noch swapon device benutzen

sed
===

* Standard : _sed -e 's/xxx/yyy/g' file_  

Da kann man sich das -e sparen    

sed kann bestimmte Dinge nur auf Teile anwenden, zum Beispiel auf bestimmte Zeilen  
    _sed -n xxx,yyyp file_ 
gibt file zwischen Zeile xxx und yyy aus, also :
    _sed -n 1,5p file_ 
ist  aequivalent zu 
    _head -5 file_
aber zu _sed -n 2,5p file_ gibts schon nix mehr...  
  

tr
==

* _tr 'c1' 'c2'_ ersetzt c1 durch c2  
* _tr -s 'c1'_  ersetzt wiederholtes Vorkommen von c1 durch ein c1   
* => _tr -s ' '_ ersetzt Spaces durch ein Space!  


join
====

* _join file1 file2_ directly joins on field1, not matching lines are omitted
* _join -a1 -a2 file1 file2_ joins ALL, but you can not tell, where something is missing
* _join -a1 -a2 -o 0 1.2 2.2 -e "---" file1 file2_ joins all and through the format -o 0 ... and the -e "---" you can tell which fields are missing.
* Problem : If you want to join consequtively more files, the format gets rather exhaustive...
* Solution: Use _auto_ for the format-Parameter -o : _join -a1 -a2 -o auto -e "---" summary-file file2_ 


LVM
===

* Step 1 : _pvcreate /dev/sdb1 /dev/sdb2 ..._  
* Step 2 : _pvscan_  
* Step 3 : _vgcreate MeinVolume /dev/sdb1  /dev/sdb2 ..._  
* Step 4 : _vgscan_  
* Step 5 : _lvcreate --size xxx --name "yyy" MeinVolume_  
* Step 6 : _lvscan_  
* Step 7 : _mkfs.ext /dev/MeinVolume/yyy_  
* Step 8 : _vi /etc/fstab_  


/etc/security/limits.d
======================

* Anzahl logins begrenzen, wirkt nur auf Login Shells, Examples selbsterklaerend


FOR-Loops
=========

    for i in {1..};   
       do echo "Hallo $i" ;   
       echo "==========" ; 
       echo " ";   
    done  



tar
===

* _tar -a ..._ detektiert den Kompressions-Algorithmus anhand der Extension  

Things to remember or check
===========================

* Backups : _tar -caf_  
* User processes : _ps, top , kill_  
* Restoring : _tar, permissions check_  
* File-permissions : _ulimits_  
* Permissions : _/etc/security/limits.d_ (pam)  
* Accessing root account : _/etc/sudoers_  
* Editing text on the command-line : _cut, cat, sed, tac, tr, ..._  
* format filesystemss: _mkfs.xxx, e2label_ ,  
* swap : _mkswap_  
* Partitioning : fdisk  
* LVM : pvcreate, vgcreate, lvcreate  

More things to remember
=======================

## Keyboard-Layout ändern
    apt-get install console-common
    install-keymap de
Oder andere keyboard-layouts in ```/usr/share/keymaps```


Backticks Replacement
=====================

Instead of backticks  
    hugo=`egon`
better use  
    hugo=$(egon)
    
Do not confuse with   
    hugo=${egon}  
which is encapsulation of shell-Variable hugo, which you normally would adress with $hugo

ssh-access without password
===========================

* see [this site here: http://www.linuxproblem.org/art_9.html](http://www.linuxproblem.org/art_9.html)
* or use : _ssh-copy-id user@server_ if you have a pub-key

Administrating several hosts
============================

* ```clusterssh```
* ugly but cool
* or use instead (if anyway already using tmux...) : ```tmux-cssh``` from e.g. /github.com/zinic



Disk-Speed
==========

* use dd
* eg: ```dd if=/dev/zero of=file_on_disk_to_test bs=1M count=1024 status=progress```
* use ```conv=fdatasync``` as option to sync already with dd, so the statistik printed out is right


Echo vs Sudo
============

* sudo -i , then the echo
* sudo sh -e "echo and here ist starts to get complicated because of escape 
* echo "xxx " > uuuu => echo "xxx " | sudo tee uuuu 

