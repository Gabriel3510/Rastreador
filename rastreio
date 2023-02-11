//Programa: Localizacao GPS com modulo SIM808 Arduino
//Autor: Gabriel Lima e Higor Barbosa 
#include <Adafruit_FONA.h>
#include <SoftwareSerial.h>
#define SIM808_RX 2
#define SIM808_TX 3
#define SIM808_RST 4
SoftwareSerial SIM808SS = SoftwareSerial(SIM808_TX, SIM808_RX);
SoftwareSerial *SIM808Serial = &SIM808SS;
Adafruit_FONA SIM808 = Adafruit_FONA(SIM808_RST);
void setup()
{
 Serial.begin(9600);
 Serial.println(F("Teste basico do modulo SIM808"));
 Serial.println(F("Inicializando... (pode demorar alguns segundos)"));
 //Inicializa o SIM808 com velocidade de comunicacao 9600bps
 SIM808Serial->begin(9600);
 //Inicia o modulo
 SIM808.begin(*SIM808Serial);
 Serial.println("Modulo inicializado!");
}
void loop()
{
 //Mostra o IMEI do modulo
 char imei[16] = {0};
 uint8_t imeiLen = SIM808.getIMEI(imei);
 if (imeiLen > 0) {
   Serial.print("Numero IMEI do modulo: ");
   Serial.println(imei);
   Serial.println();
 }
 //Liga o GPS do modulo
 if (!SIM808.enableGPS(true))
   Serial.println(F("Failed to turn on"));
 //Mostra a localizacao GPS
 char gpsdata[120];
 SIM808.getGPS(0, gpsdata, 120);
 Serial.println();
 Serial.println(F("Formato: mode,fixstatus,utctime(yyyymmddHHMMSS),latitude,longitude,altitude,speed,course,fixmode,reserved1,HDOP,PDOP,VDOP,reserved2,view_satellites,used_satellites,reserved3,C/N0max,HPA,VPA"));
 Serial.print("Dados do GPS: ");
 Serial.println(gpsdata);
 //Aguarda 5 minutos e repete o processo
 Serial.println();
 delay(300000);
}
