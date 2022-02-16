# Z-Stack-firmware
This repository contains compilation instructions and compiled Z-Stack firmwares for the Texas Instruments CC2530, CC2531, CC2538, CC1352P, CC2652P, CC2652R and CC2652RB.

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
