K1

Zum Kapitel K1 gibt es nicht viel zu schreiben, da wir dies bereits bei der LB1
beschrieben und dokumentiert haben. Hier geht es schliesslich nur darum die
Programme zu installieren.

K2

Github Accound sowie Git-Client sind bereits installiert und eingerichtet. Dass
die Dokumentation als Markdown vorhanden ist, ist anschliessend auch
selbstverständlich.

Kommen wir nun dementsprechend zu unserem Wissensstand:

Unser Wissenstand war bevor wir diese Lernbeurteilung bestritten haben, was das
Thema Containirisierung angeht, sehr tief. Wir hatten sowas nie gemacht davor
und wussten daher auch so gut wie nichts davon, beziehungsweise wie man das zu
machen hat.

Was wir aber sagen müssen bezüglich Lernschritte, dass wir vieles gelernt und
erlernt haben. Wir wissen einiges im Gegensatz zu dem Stand davor.

K3

Kommen wir zum wirklich spannenden Teil: K3

Hier geht es darum Docker Container zu kombinieren beziehungsweise einen
Bakcend, und Frontend einzusetzen. Die Desktop-App die bei uns als Frontend
eingesetzt wurde, war OSTicket. Im Hintergrund dazu haben wir eine SQL, die die
ganzen Daten dazu speichert und aufnimmt.

Wie wir dies genau gemacht haben hier im Anschluss:

Als erstes musste MySQL installiert werden, dazu gehört auch Passwort etc.
mitzugeben:

docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret -e
MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mysql:5

Anschliessend logischerweise noch OSTicket, welches an die Datenbank angehängt
und verknüpft wird:

docker run --name osticket -d --link osticket_mysql:mysql -p 8080:80
campbellsoftwaresolutions/osticket

Kommen wir zum sogenannten Volume. Hier geht es darum, die Volumes also die
Pfade abzuändern, daher wollen wir beispielsweise das ganze bei uns Lokal
abspeichern. Leider hatten wir Probleme (wir haben dies auch mit Herrn Bernet
angeschaut). Es ist weder bei Git Bash weder noch bei Powreshell gegangen. Hier
aber dennoch den Befehl dafür:

docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret -e
MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mysql:5
-v C:\\DOCKER\\container\\mysql:/var/lib/mysql

Was damit gewollt ist, die ganzen SQL Dateien im C:\\Docker\\container\\mysql
abzuspeichern.

K4

Kommen wir zum Sicherheitspart:

Um die Überwachung gewährleisten zu können, haben wir uns das Tool PRTG
heruntergeladen. Mit diesem ist es möglich die ganze Umgebung von Docker zu
überwachen und allenfalls auch per Benachrichtigung steuern zu lassen. Wir haben
logischerweise nur eine Testversion, das Produkt würde nach ein paar Monaten
etwas kosten.

Weitere drei Absicherungen für den Container zur zusätzlichen Sicherheit konnten
wir wie folgt integrieren:

Speicher begrenzen:

docker run -m 128m --memory-swap 128m amouat/stress stress --vm 1 --vm-bytes
127m -t 5s

CPU Einsatz:

docker run -d --name load1 -c 2048 amouat/stress

docker run -d --name load2 amouat/stress

docker run -d --name load3 -c 512 amouat/stress

docker run -d --name load4 -c 512 amouat/stress

docker stats \$(docker inspect -f {{.Name}} \$(docker ps -q))

Neustarts begrenzen:

docker run -d --restart=on-failure:10 my-flaky-image

Reflexion:

Kommen wir zum Schluss noch zur Reflexion.  
Wir haben uns über das gesamte Projekt sehr Mühe gegeben (trotzdem viel es uns
besonders anfangs etwas schwer). Wir kamen zum Beginn noch nicht so gut zurecht
mit dem ganzen «anders Denken» mit der Containirisierung etc….

Das Ganze macht aber Spass und vor allem da es für die Zukunft extrem von
Bedeutung hat, und immer mehr kommen wird, haben wir uns sehr Mühe gegeben und
wollten eine gute Note und somit ein gutes Resultat erzielen.

Wir sind insgesamt zufrieden und finden es ein wichtiges und lehrreiches Modul,
es ist sehr aktuell und «lebt im Heute». Das was man hier lernt, kann man gut
gebrauchen und hat potenzial für die Praxis.
