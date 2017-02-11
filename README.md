# nab_mqtt
nabaztag with mqtt


Per fare diventare il coniglio una periferica per mqtt bisogna al boot
fargli leggere il codice modificato
purtroppo quindi serve, almeno all'avvio, un server web dal quale fare caricare tale codice

copiate i files nella cartella radice del server

bc.jsp
macaddressconiglio.jsp   *vedi sotto

entrate nella configurazione del coniglio e impostate come server l'indirizzo del server web 

per esempio http://192.168.1.10

salvate e riavviate il coniglio

fatto

*file di configurazione:

macaddressconiglio.jsp


campi separati da uno spazio

mqtt_port porta del server broker
mqtt_broker nome del server broker con la porta di connessione ( https://www.cloudmqtt.com/ offre un servizio free o anche http://www.mqtt-dashboard.com/)
mqtt_user eventuale utente
mqtt_password eventuale password
mqtt_clientID nome del client mqtt deve essere unico per server (se non specificato usa il mac address del coniglio)
mqtt_topic topic dei comandi da inviare (se non specificato usa il mac address più /in: /123456789012/in)
mqtt_topic_out topic dei comandi che il coniglio invia (se non specificato usa il mac address più /out: /123456789012/out)
clock 1 attiva orologio (segnala ad ogni ora) - 0 niente orologio
alarm 1 attiva la sveglia - 0 sveglia non attiva
clock_msg specifica il messaggio per ogni ora (se non specificato emette un suono)
tts_url indirizzo per trasformare testo in mp3 (es: http://www.voicerss.org/ offre un servizio gratuito bisogna registrarsi e inserire la key e gli altri parametri nell'url)
alarm_msg messaggio della sveglia (se non specificato emette un suono)
time_clock imposta ora formato hhmmss ora minuti secondi senza spazi se impostate il server ntp non usatelo
alarm_clock imposta sveglia hhmmss
sleep_clock imposta l'ora della nanna hhmmss
wakeup_clock imposta l'ora della sveglia hhmmss
ojn_url http://openznab.it/ojn/FR/api.jsp?sn=macaddressbunny=13287162317639162376273678236722& server openjabnab parte fissa, al quale poter mandare comandi violet
ntp_server ip del server ntp
tmz numero timezone
tms segno + o - timezone
b1_topic (topic per quando si preme il bottone, 1 click)
b1_msg (messaggio per quando si preme il bottone, 1 click)
b2_topic (topic per quando si preme il bottone, 2 click)
b2_msg (messaggio per quando si preme il bottone, 2 click)
ears_topic (topic per quando si muovono le orecchie)
ears_msg (messaggio per quando si muovono le orecchie)
rfid1 (codice rfid)
rfid1_topic (topic per quando annusa rfid1)
rfid1_msg (messaggio per quando annusa rfid1)



esempio: 123456789012.jsp

mqtt_port 19129
mqtt_broker m10.cloudmqtt.com:19129
mqtt_user donald
mqtt_password duck
clock 1
alarm 1
clock_msg MSG=IT+IS+
tts_url http://api.voicerss.org/?key=xxxxxxxxxxxxx&r=-3&hl=en-gb&f=16khz_8bit_stereo&src=
alarm_msg MSG=Remember+you+have+to+go+to+work;
time_clock TIME=193500
alarm_clock ALARMCLOCK=115700
sleep_clock SLEEPTIME=210000
wakeup_clock WAKEUPTIME=083000
ojn_url http://openznab.it/ojn/FR/api.jsp?sn=macaddressbunny=13287162317639162376273678236722&
rfid1 012345678d87d
rfid1_msg MSG=Pfuiiiii!!!;
ntp_server 91.201.56.201
tmz 1
tms +

ricordatevi di personalizzare la lingua nel tts_url

varie:

comandi inviabili tramite client mqtt al topic (per esempio) /123456789012/in

EARS;R=1;L=2; (muove le orecchie right di 1 e left di 1)
TIME=100000 (imposta l'orologio alle 10 00 00)
SLEEPTIME=201200 (imposta l'ora per andare a letto alle 20 12 00)
WAKEUPTIME=080200 (imposta l'ora in cui si sveglia alle 08 02 00)
ALLARMCLOCK=130000 (imposta l'ora della sveglia alle 13 00 00)
AMSG=MSG=YUPPY! (imposta il messaggio da inviare per la sveglia)
RD=http://str01.fluidstream.net:7020; (attiva la radio dal sito)
MSG=BLABLABLA (dice blablabla)
MP3=http://miosito.com/x.mp3 (suona il brano mp3 dal sito)
BOOT; (esegue il pacchetto di boot .. reset)
WAKEUP; (alzati!)
SLEEP; (dormi!)
TAICHI=255 (imposta la frequenza del taichi da 0=niente a 255=molto)
RAW=0000 (pacchetto grezzo vedi *)
BREATH=5 (colore respirazione da 0 a 7)
NOSE=0 (lampeggio naso 0 no 1 un lampeggio 2 doppio lampeggio)
TIME? dice ora minuti e secondi attuali
OJN=tts=Buongiono+sono+io invia al server openjabnab il comando tts etc



