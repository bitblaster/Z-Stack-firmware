# Z-Stack-firmware
This repository contains compilation instructions and compiled Z-Stack firmwares for the Texas Instruments CC2530, CC2531, CC2538, CC1352P, CC2652P, CC2652R and CC2652RB.
------------------------------------------------------------------------------------------------------

# Hardware
Ho acquistato il modulo EBYTE E72-2G4M20S1E (~6 euro), quindi [ho progettato su EasyEDA un PCB](https://easyeda.com/editor#id=80087430ce2c4b63b9acd52e8b4b1f77) con un header JTAG, uno UART e due pulsanti (Reset e Flash), secondo le indicazioni di [questo sito](https://github.com/egony/cc2652p_E72-2G4M20S1E/wiki/Home-EN)

Schema
![image](https://user-images.githubusercontent.com/701527/154369845-40900dd8-8c42-4440-8fab-89a9bb422eb9.png)


PCB - versione header in basso
![image](https://user-images.githubusercontent.com/701527/154369612-9471e3ae-cbd4-4f1b-80e2-b94034dfbeb0.png)

PCB - versione header su lati opposti
![image](https://user-images.githubusercontent.com/701527/154369638-d11d70cb-b1a9-409c-b93f-fb45949f231a.png)

# Flashing
Per il mio (EBYTE E72-2G4M20S1E con chip CC2652P), ho usato il fw coordinator/Z-Stack_3.x.0/bin/CC1352P2_CC2652P_other_coordinator_20211217.zip

Per il flashing ho usato il metodo tramite UART FT232 e bootloader (che era presente nel mio device).
Sw utilizzato: [SmartRF Flash Programmer v2](https://www.ti.com/tool/FLASH-PROGRAMMER) su Windows.
Ho cercato alternative per Linux, ma senza successo:
- OpenOCD: non sono riuscito a capire come si usa (se si può) tramite FT232
- [cc2538-bsl](https://github.com/JelmerT/cc2538-bsl): sembra funzionare, ma di una lentezza devastante (circa 40min per la lettura). Inoltre facendo il verify di quanto appena flashato mi dava errore CRC, quindi non sono nemmeno sicuro che fosse affidabile.

Da provare flashing tramite JTAG, sembra che il device che va per la maggiore sia Segger J-Link, anche se c'è un progetto (open?) che si chiama Black Magic Pro che dovrebbe funzionare ugualmente, entrambi tramite OpenOCD.

Per verificare che il coordinator funzionasse, ho creato un server MQTT di test Mosquitto e un server zigbee2mqtt (v. file in questo repo).
Avviare prima il server MQTT con "docker-compose up", quindi, allo stesso modo, il server zigbee2mqtt.

Se tutto va bene si dovrebbe vedere dal log di zigbee2mqtt il collegamento al device e l'attivazione del permit join automatica.
Si dovrebbe quindi riuscire ad accoppiare dei dispositivi.
