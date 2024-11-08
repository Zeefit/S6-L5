ho testo oggi come fare il craking dell'username e passowrd usando un attacco a dizionario sul un utente di prova che ho creato chiamato "test_user" ,ho iniziato scrivendo sudo adduser test_user (serve a creare un nuovo utente) poi ho fatto sudo service ssh start(per startare il protocollo ssh)
e ho fatto l'accesso al nuovo utente ssh facendo "ssh test_user@192.168.1.218" riuscendo a stabilire la connessione,dopodichè ho inziato ad eseguerei l'attacco,scrivendo 
"hydra -L /home/kali/Desktop/user.txt -P /home/kali/Desktop/rockyou.txt 192.168.1.218 -t1 ssh" (ho messo -t1 per avere un tempo più lento ed evitare che il sistema blocchi l'attacco) in questo caso nel codice -L e -P stanno per 
-L è l'opzione per specificare un file contenente un elenco di nomi utente
-P è l'opzione per specificare un file contenente un elenco di password
-t imposta il numero di task (thread) in questo caso 1
a fine del processo ho ottenuto le credenziali in chiaro
ho rifatto la stessa cosa cambiando la fine in "hydra -L /home/kali/Desktop/user.txt -P /home/kali/Desktop/rockyou.txt 192.168.1.218 -t1 ftp"(prima usavo il protocollo ssh su porta ) facendo cosi lo stesso attacco su l'utente ftp e ottenendo comunque le credenziali in chairo,prima però  ,scaricato in precedenza il servico facendo sudo apt-get install vsftpd
ho configuranto il file di configurazione ftp attivando :
local_enable=YES: Consente l'accesso tramite FTP per gli utenti locali del sistema
write_enable=YES: Permette agli utenti di caricare file sul server FTP(come in un vero scenario)
