Oggi ho testato come effettuare il cracking dell'username e della password utilizzando un attacco a dizionario su un utente di prova che ho creato, chiamato "test_user". Ho iniziato scrivendo sudo adduser test_user (serve a creare un nuovo utente), poi ho eseguito sudo service ssh start (per avviare il protocollo SSH). Successivamente, ho effettuato l'accesso al nuovo utente SSH usando ssh test_user@192.168.1.218, riuscendo a stabilire la connessione. Dopodiché, ho iniziato a eseguire l'attacco, scrivendo:

hydra -L /home/kali/Desktop/user.txt -P /home/kali/Desktop/rockyou.txt 192.168.1.218 -t1 ssh

Ho messo -t1 per avere un tempo più lento ed evitare che il sistema blocchi l'attacco. In questo caso, nel codice:

-L è l'opzione per specificare un file contenente un elenco di nomi utente.
-P è l'opzione per specificare un file contenente un elenco di password.
-t imposta il numero di task (thread), in questo caso 1.

Alla fine del processo, ho ottenuto le credenziali in chiaro. Ho rifatto la stessa procedura cambiando la parte finale in:


hydra -L /home/kali/Desktop/user.txt -P /home/kali/Desktop/rockyou.txt 192.168.1.218 -t1 ftp
Prima utilizzavo il protocollo SSH su porta, e in questo caso ho fatto lo stesso attacco sull'utente FTP, ottenendo comunque le credenziali in chiaro. Prima di questo, avevo scaricato il servizio con il comando sudo apt-get install vsftpd.

Ho poi configurato il file di configurazione FTP attivando:

local_enable=YES: consente l'accesso tramite FTP per gli utenti locali del sistema.
write_enable=YES: permette agli utenti di caricare file sul server FTP (come in un vero scenario).
