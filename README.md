# nab_mqtt
nabaztag with mqtt protocol

if for example:

your bunny macaddress is: 123456789012
your pc ip is: 192.168.2.5

donwload mosquittobroker server install and run
your server broker will be 192.168.2.5:1883

download a web server and run
your server www will be 192.168.2.5:80

download boot code bc.jsp and create a config file (below)
and copy in web server root

enter in configuration of your  bunny and set url config with
http://192.168.2.5:80

update
for boot version 6
add for config file

mqtt_conn_topic on connect topic
mqtt_conn_msg on connect message
parameters default 110001-000-0-0


// ****   explain
//  parameters  110011-000-0-1
//              !!!!!! !!! ! !____ msg on connect 0 or 1
//              !!!!!! !!! !____ QoS on SUBSCRIBE 0 1 or 2
//              !!!!!! !!!____ dup on PUBLISH 0 or 1
//              !!!!!! !!____ QoS on PUBLISH 0 1 or 2
//              !!!!!! !____ retain on PUBLISH 0 or 1     
//              !!!!!!____________________ clean on CONNECT 0 or 1
//              !!!!!_____________ will flag on CONNECT 0 or 1
//              !!!!___________ will QoS on CONNECT 0 1 or 2
//              !!!_________ will retain on CONNECT 0 or 1
//              !!_______ password on CONNECT 0 or 1
//              !____ user on CONNECT 0 or 1
example
parameters 110011-000-0-1
(mqtt broker with user and password with clean on CONNECT and will message and msg on connect)

new commands sent via mqtt topic /123456789012/in
REBOOT; for reset bunny




for boot version 5
config parameters


ping	ip where send record file
mqtt_port	port server broker
mqtt_broker	server broker with port
mqtt_user	user server broker
mqtt_password	password server broker
mqtt_clientID	unique client mqtt name (default mac address)
mqtt_topic	topic input (default macaddress + /in)
mqtt_topic_out	topic output (default macaddress + /out)
clock	1 clock enabled 0 clock disabled
alarm	1 alarm enabled 0 alarm disabled
clock_msg	msg for clock hour
tts_url	url for tts
alarm_msg	msg for alarm
time_clock	set time clock
alarm_clock	set alarm clock
sleep_clock	set sleep clock
wakeup_clock	set wakeup clock
ojn_url	url server ojn + parameters
ntp_server	ip server ntp
tmz	number timezone
tms sign	+/- timezone
b1_topic	topic for 1 click button
b1_msg	msg for 1 click button
b2_topic	topic for 2 click button
b2_msg	msg for 2 click button
ears_topic	topic for ears move
ears_msg	msg for ears move
rfid	list of codes rfid separated by the character $
rfid_topic	list of topic separated by the character $
rfid_msg	list of msg separated by the character $
rss1	url for rss
rrs1title	number of titles to be read
month	list of month name separated by the character $
mqtt_will_topic	testament topic
mqtt_will_msg	testament message

example file
123456789012.jsp

ping 192.168.2.5
mqtt_broker 192.168.2.5:1883
mqtt_port 1883
clock 1
alarm 0
clock_msg MSG=It+is+
tts_url http://api.voicerss.org/?key=00000000000000000000000000000000&r=0&hl=en-gb&f=44khz_16bit_stereo&src=
alarm_clock ALARMCLOCK=180200
sleep_clock SLEEPTIME=2201000
wakeup_clock WAKEUPTIME=065800
ntp_server 91.201.56.201
tmz 1
tms +
month January$February$March$April$May$June$July$August$September$October$November$December
rss1 http://www.ansa.it/sito/notizie/politica/politica_rss.xml
rss1title 4
rfid d00218c1090b1230$d0021a0352c14123$d00218c123163e94$d00123c109163a2b
rfid_topic /123456789012/in$/123456789012/in$/123456789012/in$/123456789012/in
rfid_msg MSG=Bunny+green$MSG=Bunny+dark+green$MSG=Stamp+red$MSG=Stamp+yellow
mqtt_will_topic /info
mqtt_will_msg offline



commands sent via mqtt topic /123456789012/in

EARS;R=1;L=2; (move ears right 1 and left 1)
ALLARMCLOCK=130000 (set alarm clock 13 00 00)
AMSG=MSG=YUPPY! (set message for alarm)
RD=http://str01.fluidstream.net:7020; (enable stream radio from url)
MSG=Blabla (say blabla)
MP3=http://192.168.2.5/x.mp3 (play mp3 from url)
BOOT; (reset led and ears)
WAKEUP;
SLEEP;
TAICHI=255 (set taichi frequency  0=nothing  255=often)
RAW=0000 (*)
BREATH=5 (breath color 0-7)
NOSE=0 (nose blink 0, 1 blink, 2 blink)
TIME? say hour minuts seconds
DATE? say day month year
OJN=tts=Blabla send to ojn server the command violet for tts
RSS1; read rss1 stream
RSS1TITLE=2 set 2 title to read from rrs
TEST=1 emulates 1,2 or 3 physical click (3 is for record voice)

* RAW Values

like the original nabaztag:

Service_Weather
010x Weather_Sun = 0, Weather_Cloudy = 1, Weather_Smog = 2, Weather_Rain = 3, Weather_Snow = 4, Weather_Storm = 5

Service_StockMarket
020x StockMarket_HighDown = 0, StockMarket_MediumDown = 1, StockMarket_LittleDown = 2, StockMarket_Stable = 3, StockMarket_LittleUp = 4, StockMarket_MediumUp = 5, StockMarket_HighUp = 5

Service_Periph
030x Periph_VeryLow = 0, Periph_Low = 1, Periph_LowAverage = 2, Periph_Average = 3, FastAverage = 4, Fast = 5, VeryFast =6

Service_EMail
040x EMail_No = 0, EMail_1 = 1, EMail_2 = 2, EMail_3AndMore = 3

Service_AirQuality
050x AirQuality_Good = 0, AirQuality_Medium = 5, AirQuality_Bad = 10

000x disable service x.. 1, 2, 3, 4, 5






