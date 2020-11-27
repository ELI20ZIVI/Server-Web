# Readme Server Web

Una volta importata la macchina virtuale si setta la scheda di rete su BRIDGE 

(la macchina è vista dal router come un computer fisico vero e proprio)

- Impostazioni

- Scheda di rete

- La si setta su BRIDGE (in origine è settata su NAT)
  
  

Impostare l'indirizzo IP statico (fondamentale per visualizzare il sito dall'esterno)

- aprire con l'editor di testo il file **netplan** con il **comando sudo nano /etc/netplan**

- settare il file netblan con l'**indirizzo IP**, la **netmask**, il **gateway** e il **DNS**

- riavviare la macchina virtuale

---

CHECKPOINT

Controllare con il comando **ifconfig** se l'indirizzo IP mostato nel file della configurazione è uguale a quello che la macchina riporta come output del comando

---



Installare un server SSH in modo da controllare la macchina da remoto (opzionale - solo per il controllo remoto della macchina virtuale, non necessario al funzionamento del server web)

- digitare nel terminale il seguente comando **sudo apt install openssh-server**

- dal prossimo riavvio ho la possibilità di accedere da ssh

---

CHECKPOINT

Dal pc fisico avviare un ssh client (PuTTY è uno) e provare a connettersi alla macchina virtuale

---



Installare il server web vero e proprio con apache

- digitare nel terminale il seguente comando **sudo apt install apache2**

- riavviare la macchina per apportare le modifiche

- aprire il file manager e andare nella cartella /var/www/html per visualizzare la pagina index.html

- se questa cartella esiste il server web è stato installato correttamente

---

CHECKPOINT

Provare a digitare l'indirizzo IP della macchina virtuale sul browser della macchina fisica per controllare se viene visualizzato il sito di esempio di apache

---



Modificare la pagina index.html

- Aprire conm un editor di testo la pagina index.html con il comando **sudo nano /etc/www/html/index.html**

- impostare ed editare la pagina a piacere

---

CHECKPOINT

Provare a digitare l'indirizzo IP della macchina virtuale sul browser della macchina fisica per controllare se viene visualizzato il sito di modificato

Se il sito non viene visualizzato o viene visualizzato qualche errore provare a controllare la configurazione di rete o la pagina html editata in precedenza

---



Configurazione di più pagine su un web server

- aprire la cartella /etc/apache2/sites-available con il comando **cd /etc/apache2/sites-available**

- per la configurazione di un altro sito devo creare un file di configurazione che creo con il comando **sudo touch 0x0-default.conf** (x da sostituire con il numero della configurazione)

- per semplicità si copia il contenuto del file di configurazione 000-default.conf con **sudo nano 000-default.conf** e copiando il suo contenuto

- incollare il contenuto del file aperto con nano (000-default.conf) nel file creato precedentemente (0x0-default.conf) e editare a seconda delle esigienze

- una volta finito di settare il file di configurazione uscire dall'editor e dare il comando **a2ensite 0x0-default.conf** sul terminale

- configurare **server name**, **cartella di root del sito** e le varie **cartelle di log**

- do il comando **systemctl reload apache2** per applicare le modifiche

- provare su un browser da una macchina host se i vari siti sono raggiungibili

- se non si raggiungono i siti controllare la configurazione di rete o la configurazione del server

---

CHECKPOINT

Digitare i vari server name nella balla di ricerca del browser della macchina fisica e controllare che tutti i siti siano raggiungibili

---



Installazione server FTP

- creare il nuovo utente amministratore con il comando **sudo useradd -s /bin/bash -d /var/www/'Sito A' -m usersitoa** e impostare la password con il comando **sudo passwd usersitoa**

- installare il server FTP con il comando **sudo apt install vsftpd** sulla macchina linux

- settare il file di configurazione del file FTP per il corretto funzionamento

- installare un client FTP sulla macchina dell'amministratore (es. FileZilla) e avviarlo

- effettuare il login sul client e provare il trasferimento dei file dal client al server (se non dovesse funzionare controllare le impostazioni del server web e del server FTP)

---

CHECKPOINT

Aprire un FTP client sulla macchina fisica e, una volta eseguito il login, provare a vedere se è possibile lavorare con i file

---



Se non è possibile raggiungere i siti è probabile che vada settato il DNS locale sulla macchina fisica

Configurazione DNS locale (su Windows)

- navigare nella cartella **C:\Windows\system32\drivers\etc\hosts**

- modificare le impostazioni del file (indirizzoIP    hostname) e salvare il file

- testare il funzionamento del dns insrendo nel browser l'hostname inserito nel file hosts

---

CHECKPOINT

digitare il sito sul browser della macchina fisica e controllare che questo sia raggiungibile

---
