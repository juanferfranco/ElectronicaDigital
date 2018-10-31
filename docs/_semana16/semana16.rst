Semana 16
===========
Durante esta semana se presentarán avances del proyecto final y se realizarán asesorías. La entrega final del proyecto 
será el viernes de esta semana.

Para la entrega considere los siguientes asuntos:

* Evaluación práctica (40%). Realizar un demo con las siguientes consideraciones: 

    * El proyecto debe tener al menos un sensor y un actuador (10%). 
    * Debe enviar la información del sensor a internet (10%).
    * Se debe poder controlar el actuador desde internet (10%). 
    * Debe generar notificaciones en base a valores críticos del sensor (10%).
    * El dispositivo debe interactuar con algún servicio web (10%).
    * Debe tener al menos dos ESP8266 que interactuen entre ellos por WiFi (machine to machine) (20%). 
    * Todos los items anteriores deben estar correctamente integrados en una aplicación con su respectivo DEMO (30%).

* Evaluación teórica (20%). Se debe entregar un informe con las siguientes consideraciones:

    * Descripción de la aplicación (5%).
    * Diagrama en bloques del sistema (5%).
    * Descripción de cada bloque (5%).
    * Explicación detallada del funcionamiento del sistema (20%).
    * Explicación detallada del código fuente de cada ESP8266 utilizado (20%).
    * Un tutorial que explique paso a paso cómo reproducir el proyecto y cómo realizar el despliegue del DEMO (20%).
    * Enlace a un vídeo que muestre el DEMO en funcionamiento (25%)

Códigos ejemplo para el trabajo final
---------------------------------------

Beacon 
^^^^^^^^
Este código está implementado para un `simblee <https://www.simblee.com/>`__.

.. code-block:: cpp 
   :lineno-start: 1

   #include <SimbleeBLE.h>
   
   // pin 3 on the RGB shield is the green led
   int led = 3;
   
   // interval between advertisement transmissions ms (range is 20ms to 10.24s) - default 20ms
   int interval = 675;  // 675 ms between advertisement transmissions
   
   void setup() {
     // led used to indicate that the Simblee is advertising
     pinMode(led, OUTPUT);
   
     SimbleeBLE.deviceName = "Perro";
   
     // this is the data we want to appear in the advertisement
     // (if the deviceName and advertisementData are too long to fix into the 31 byte
     // ble advertisement packet, then the advertisementData is truncated first down to
     // a single byte, then it will truncate the deviceName)
     SimbleeBLE.advertisementData = "012345";
     
     // change the advertisement interval
     SimbleeBLE.advertisementInterval = interval;
   
     // start the BLE stack
     SimbleeBLE.begin();
   }
   
   void loop() {
     // switch to lower power mode
     Simblee_ULPDelay(INFINITE);
   }
   
   void SimbleeBLE_onAdvertisement(bool start)
   {
     // turn the green led on if we start advertisement, and turn it
     // off if we stop advertisement
     
     if (start)
       digitalWrite(led, HIGH);
     else
       digitalWrite(led, LOW);
   }

BLE Scanner
^^^^^^^^^^^^
Este ejemplo escrito para un ESP32 permite detectar la presencia de de un beacon, en particular, el beacon del ejemplo anterior.

.. code-block:: cpp 
   :lineno-start: 1

   #include <BLEDevice.h>
   #include <BLEUtils.h>
   #include <BLEScan.h>
   #include <BLEAdvertisedDevice.h>
   
   int scanTime = 2; //In seconds
   
   uint8_t scanPerro = 0;
   
   class MyAdvertisedDeviceCallbacks: public BLEAdvertisedDeviceCallbacks {
       void onResult(BLEAdvertisedDevice advertisedDevice) {
         std::string dataRX = advertisedDevice.toString();
   
         //Serial.printf("Advertised Device: %s \n", dataRX.c_str());
         //Serial.println("----------------------------------------------------");
         int32_t  n = dataRX.find("Perro");
         if (n != -1) scanPerro = 1;
   
         //Serial.println(n);
         //Serial.println();
         //Serial.println("***********************************************");
       }
   };
   
   void setup() {
     Serial.begin(115200);
   }
   
   void loop() {
     // put your main code here, to run repeatedly:
     scanPerro = 0;
     beaconScan();
     //delay(2000);
   }
   
   void beaconScan() {
     Serial.println("Scanning...");
     BLEDevice::init("");
     BLEScan* pBLEScan = BLEDevice::getScan(); //create new scan
     pBLEScan->setAdvertisedDeviceCallbacks(new MyAdvertisedDeviceCallbacks());
     pBLEScan->setActiveScan(true); //active scan uses more power, but get results faster
     BLEScanResults foundDevices = pBLEScan->start(scanTime);
     if (scanPerro == 1) {
       Serial.println(" Perro is Here! ");
     }
     else {
       Serial.println(" Where is Perro :( ");
     }
     Serial.println("Scan done!");
   }

Sensor de movimiento: PIR 
^^^^^^^^^^^^^^^^^^^^^^^^^^

* En `este <https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/how-pirs-work>`__ enlace podrán encontrar 
  información acerca del funcionamiento y prueba de un sensor PIR.
* En `este <https://www.didacticaselectronicas.com/index.php/sensores/sensor-de-movimiento,-pir-sensor,-pir-detail>`__ 
  enlace se puede encontrar la información para comprar el sensor PIR.