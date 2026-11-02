
# SYTB
- Scripts
- Ilijas Petricevic
- 3AHITS
- 02.11.26

---

## Übung (Directory Struktur)

Schreibe ein Shell-Script das Unterverzeichnisse und Dateien anlegt, es wird ein Argument an das Script übergeben.

**Aufruf:**
```sh
./build_dirs.sh abcd
```

Dies führt zu folgender Directorystruktur:
```sh
./
└── abcd/
    ├── abcd_01/
    │   ├── abcd.01.1.txt
    │   ├── abcd.01.2.txt
    │   └── abcd.01.3.txt
    └── abcd_02/
        ├── abcd.02.1.txt
        ├── abcd.02.2.txt
        └── abcd.02.3.txt
```
Schreibe weiters ein Shell-Script clean_dir.sh das diese Verzeichnisstruktur wieder löscht.<br>


**In build_dirs.sh:**
```sh
#!/bin/bash

name="$1"

mkdir -p "$name"

for i in 01 02
do
    mkdir -p "$name/${name}_${i}"

    for j in 1 2 3
    do
        touch "$name/${name}_${i}/${name}.${i}.${j}.txt"
    done
done
```

**In shell:**
```sh
chmod +x build_dirs.sh
./build_dirs.sh abcd
tree abcd
```

### clean_dir.sh:
```sh
touch clean_dir.sh
```

**In clean_dir.sh**
```sh
#!/bin/bash

rm -r "$1"
```

**In shell**
```sh
chmod +x clean_dir.sh
./clean_dir.sh abcd
```

---

## Übung (Skript Generator)

Schreibe ein Skript das

- eine Skriptdatei erzeugt (Name wird als Argument übergeben),
- die She-Bang Zeile einfügt,
- einen echo Befehl einfügt und
- das eXecution Flag für das Skript setzt.

Anwendung:
```sh
$ ./makescript.sh mytest
```

erzeugt die Datei mytest.sh:
```sh
#!/bin/sh
echo "mytest Skript"
# write yor script here
```

Das Skript kann sofort ausgeführt werden:
```sh
$ ./mytest.sh
```

### make_script.sh
```sh
touch make_script.sh
```

**In make_script.sh**
```sh
#!/bin/bash

touch "$1.sh"
chmod +x "$1.sh"
echo "#!/bin/sh" >> "$1.sh"
echo "echo \"$1 Skript\"" >> "$1.sh"
echo "# write yor script here" >> "$1.sh"`
```

**In shell**
```sh
chmod +x makescript.sh
./makescript.sh test
./test.sh
```

**Ausgabe**
```
test Skript
```

---

## Übung (Headline Cat)

Verwende ```$@``` zur Lösung dieser Aufgabenstellung.

Schreibe ein Skript das eine Art cat zur Verfügung stellt. Als Argumente werden eine beliebige Anzahl von Textdateien übergeben. Das Ergebnis wird in die Datei result.txt geschrieben (ist die Datei vorhanden soll deren Inhalt überschrieben werden). Jedem Datei-Inhalt soll eine Überschrift vorangestellt werden.

Beispiel – der Aufruf
```sh
$ ./headline_cat.sh file1.txt file2.txt file3.txt
```
ergibt die Datei result.txt mit folgendem Inhalt:
```sh
== file1.txt ==========================================
Das ist der Inhalt
der ersten Textdatei

== file2.txt ==========================================
Das ist der Inhalt
der zweiten Textdatei

== file3.txt ==========================================
Das ist der Inhalt
der dritten Textdatei
```

### headline_cat.sh
```sh
touch headline_cat.sh
```

**In headline_cat.sh**
```sh
#!/bin/bash

> test.txt

for file in "$@"
do
    echo "== $file ==========================================" >> test.txt
    cat "$file" >> test.txt
    echo "" >> test.txt
done
```

**In shell**
```sh
chmod +x headline_cat.sh
echo "Test1" > file1.txt
echo "Test2" > file2.txt
echo "Test3" > file3.txt
./headline_cat.sh file1.txt file2.txt file3.txt
cat test.txt
```