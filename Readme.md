# Readme Server Web

Una volta importata la macchina virtuale si setta la scheda di rete su BRIDGE 

(la macchina è vista dal router come un computer fisico vero e proprio)

- Impostazioni

- Scheda di rete

- La si setta su BRIDGE (in origine è settata su NAT)

Installare un server ssh in modo da controllare la macchina da remoto (opzionale - solo per il controllo remoto della macchina virtuale, non necessario al funzionamento del server web)

- digitare nel terminale il seguente comando **sudo apt install openssh-server**

- dal prossimo riavvio ho la possibilità di accedere da ssh

Installare il server web vero e proprio con apache

- digitare nel terminale il seguente comando **sudo apt install apache2**

- riavviare la macchina per apportare le modifiche

- aprire il file manager e andare nella cartella /var/www/html per visualizzare la pagina index.html

- se questa cartella esiste il server web è stato installato correttamente

Impostare l'indirizzo IP statico (fondamentale per visualizzare il sito dall'esterno)

- aprire con l'editor di testo il file **netplan** con il **comando sudo nano /etc/netplan**

- settarlo seguendo questo esempio

   network:
    version: 2
     renderer: networkd
      ethernets:
       eth1:
        addresses: [indirizzo_ip/netmask]
        gateway4: gateway
        nameservers:
         search: [mydomain, otherdomain]
         addresses: [dns]

   ip link set eth1 up
   ip link set eth1 down

Modificare la pagina index.html

- Aprire conm un editor di testo la pagina index.html con il comando **sudo nano /etc/www/html/index.html**

- impostare la pagina a piacere

Provare l'effettivo funzionamento del server

- dalla macchina fisica aprire il browser e digitare l'indirizzo ip della macchina

- dovrebbe aprirsi il sito index.html che si ha modificato in precedenza

- se non si apre provare a ricontrollare la configurazione di rete o del server web

Configurazione pagine del webserver

- aprire la cartella /etc/apache2/sites-available con il comando **cd /etc/apache2/sites-available**

- per la configurazione di un altro sito devo creare un file di configurazione che creo con il comando **sudo touch 0x0-default.conf** (x da sostituire con il numero della configurazione)

- per semplicità si copia il contenuto del file di configurazione 000-default.conf con **sudo nano 000-default.conf** e copiando il suo contenuto

- incollo il contenuto del file aperto con nano (000-default.conf) nel file creato precedentemente (0x0-default.conf) e lo edito a seconda delle mie esigienze

- una volta finito di settare il file di configurazione esco dall'editor e do il comando **a2ensite 0x0-default.conf** sul terminale

- do il comando **systemctl reload apache2** per applicare le modifiche

- provare su un browser da una macchina host se i vari siti sono raggiungibili

- se non si raggiungono i siti controllare la configurazione di rete o la configurazione del server
