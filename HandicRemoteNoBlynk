// Copyright 2009 Ken Shirriff, http://arcfn.com
// Copyright 2017-2019 David Conran,
// Copyright 2021 szymonszewcjr
// 
// This is based on following demos:
// Ken Shirriff's IrsendDemo Version 0.1 July, 2009,
// IRremoteESP8266: IRrecvDumpV2,
// IRremoteESP8266: IRsendDemo,
//  
//  This sketch is supposed to be used with Esp8266 boards.
//  This sketch requires an IR Led and an IR receiver to be connected.
//  An IR LED is supposed to be driven via transistor on pin D6 on nodeMCU 1.0 (GPIO 12)
//  An output of the IR Receiver is supposed to be connected to pin D5 on on nodeMCU 1.0 (GPIO 14)
//  If you still have no clue how to wire it up, here are some further instructions:  https://github.com/crankyoldgit/IRremoteESP8266/wiki
//
//  If you need this with blynk support make sure to check out the other ino file.

#include <Arduino.h>
#include <IRremoteESP8266.h>
#include <IRrecv.h>
#include <IRsend.h>
#include <IRutils.h>

const uint16_t kRecvPin = 14;  // Pin which wil have the ir receiver connected
const uint16_t Led_pin = 12;   // Pin that has Ir led connected to it. (Might wanna use a transistor to drive the LED, because MCU can't provide enough current via its gpios)
uint32_t dane_odebrane;        // dane_odebrane stands for received_data in polish language. (too lazy to change it to smthing else)


//buttony w decimalu    (Codes to send in decimal, all those "yes" thingymajigs are my checks which i didnt delete yet)
const int mute = 77;        //1 yes
const int prech = 78;       //2 yes
const int power = 76;       //3 yes
const int input = 120;      //4 yes
const int menu = 112;       //5 yes

//dpad buttony w decimalu   (Buttons from original remotes dpad)
const int volup = 80;       //6yes
const int voldown = 81;     //7yes
const int chup = 96;        //8yes
const int chdown = 97;      //9yes
const int okbtn = 117;      //10yes
const int up = 84;          //11yes
const int down = 83;        //12yes
const int left = 85;        //13yes
const int right = 86;       //14yes

//numpad buttony w decimalu  (Buttons from number keypad of the remote)
const int num0 = 64;        //15yes
const int num1 = 65;        //16yes
const int num2 = 66;        //17yes
const int num3 = 67;        //18yes
const int num4 = 68;        //19yse
const int num5 = 69;        //20yes
const int num6 = 70;        //21yse
const int num7 = 71;        //22yse
const int num8 = 72;        //23yse
const int num9 = 73;        //24yse



IRrecv irrecv(kRecvPin);    //set receiving pin for IRrecv lib.
IRsend irsend(Led_pin);     //set led pin for IRsend lib.
decode_results results;     

void setup() {
  Serial.begin(230400);   // I have my serial baud rate this high because i got used to it, might want to change it to something more usual e.g. 115200
  irsend.begin();         // intialize the sending lib
  irrecv.enableIRIn();    // initialize and start receiving lib
  while (!Serial)         // Wait for the serial connection to be estabilished.
    delay(30);
  pinMode(2, OUTPUT);     // this is pinmode for the indicator LED, it has its own function below, can by used by calling  "indicate()"
}




//voidy własne///       (my own functions)

//indicate funtion blinks an LED on gpio 2, more of a debug thing, dunno if will be kept.
  void indicate() {
  digitalWrite(2, HIGH);
  delay(10);
  digitalWrite(2, LOW);
  }


  //function responsible for sending remote codes in easier manner, this one is strictly made for my particular TV receiver and its code types.

  void sendrc5(byte button)
  {
    irsend.sendRC5(button, 12);  //that 12 is for
  }
//koniec voidów wlasnych////////////////////////////////////// (END my oun functions)

void loop() {
    delay(30);              //initial delay to not catch any signals still bouncing around
    
if (irrecv.decode(&results)) {              //if any results found 

  dane_odebrane = results.value;            //set dane_odebrane (received_data) variable to the results
  
   serialPrintUint64(results.value);        //print whatever was found, useful when debugging or setting the detected buttons.
   Serial.println("");                      // make new line so serial monitor is readable

                     if (dane_odebrane == 4045713590 || dane_odebrane == 1863861367)  // power    // my replacement remote sent those two commands interchangably, seemingly at random, 
          {                                                                                       // here i accounted for both of them using the logical OR operator ||    
          indicate();                                                                             // what we are doing here is checking if code arrived, and if we know this code,                
          sendrc5(power);                                                                         // if above is true we call indicate() to flash an led, and we call sendrc5()
          delay(5);                                                                               // to send code to the receiver and quit the loop
          }

                      if (dane_odebrane == 3024981499 || dane_odebrane == 1863861367)  //volume UP
          {
          indicate();
          
          sendrc5(volup);
          delay(5);
          }
          
                     if (dane_odebrane == 1133087936 || dane_odebrane == 3526383262 || dane_odebrane == 902510849)  //volume DOWN
          {
          indicate();
          
          sendrc5(voldown);
          delay(5);
          }
          
                     if (dane_odebrane == 3157860949)  //chan up
          {
          indicate();
          
          sendrc5(chup);
          delay(5);
          }
          
                    if (dane_odebrane == 4289706204)  //chan down
          {
          indicate();
          
          sendrc5(chdown);
          delay(5);
          }
          
          
                    if (dane_odebrane == 544993039)  //numpad1
          {
          indicate();
          
          sendrc5(num1);
          delay(5);
          }
          
                    if (dane_odebrane == 3896860046)  //numpad2
          {
          indicate();
          
          sendrc5(num2);
          delay(5);
          }
          
                    if (dane_odebrane == 3417827657)  //numpad3
          {
          indicate();
          
          sendrc5(num3);
          delay(5);
          }
          
                    if (dane_odebrane == 740241778)  //numpad4
          {
          indicate();
          
          sendrc5(num4);
          delay(5);
          }
          
                    if (dane_odebrane == 2422134005)  //numpad5
          {
          indicate();
          
          sendrc5(num5);
          delay(5);
          }
          
                    if (dane_odebrane == 2363614204)  //numpad6
          {
          indicate();
          
          sendrc5(num6);
          delay(5);
          }
                    if (dane_odebrane == 828053765)  //numpad7
          {
          indicate();
          
          sendrc5(num7);
          delay(5);
          }
          
                    if (dane_odebrane == 3330015670)  //numpad 8
          {
          indicate();
          
          sendrc5(num8);
          delay(5);
          }
          
                    if (dane_odebrane == 3021527401)  //numpad 9
          {
          indicate();
          
          sendrc5(num9);
          delay(5);
          }
          
                    if (dane_odebrane == 990610224)  //numpad 0
          {
          indicate();
          
          sendrc5(num0);
          delay(5);
          }
          
                    if (dane_odebrane == 2029287847)  //MUTE
          {
          indicate();
          
          sendrc5(mute);
          delay(5);
          }
          
                    if (dane_odebrane == 3120614274)  //InPUT
          {
          indicate();
          
          sendrc5(input);
          delay(5);
          }


        
                    if (dane_odebrane == 3416 ||
                    dane_odebrane == 41029566 ||
                    dane_odebrane == 3372390281 ||
                    /*guzik home */ 
                    dane_odebrane == 986196487 ||
                    /*GUZIK OPTIONS*/
                    dane_odebrane == 14057)    //menu
          {
          indicate();
          
          sendrc5(menu);
          delay(5);
          }
                  
                      if (dane_odebrane == 30040)  // pre/ch btn
          {
          indicate();
          
          sendrc5(prech);
          delay(5);
          }

                      if (dane_odebrane == 1815458796)  //up btn
          {
          indicate();
          
          sendrc5(up);
          delay(5);
          }

                      if (dane_odebrane == 141285788)  //downbtn
          {
          indicate();
          
          sendrc5(down);
          delay(5);
          }

                      if (dane_odebrane == 440544835)  //left
          {
          indicate();
          
          sendrc5(left);
          delay(5);
          }

                      if (dane_odebrane == 2721830948)  //right
          {
          indicate();
          
          sendrc5(right);
          delay(5);
          }

                       if (dane_odebrane == 1922410756)  //ok btn
          {
          indicate();
          
          sendrc5(okbtn);
          delay(5);
          }        
}

delay(2);                                                                
irrecv.resume();                                                          //we need to resume the irrecv lib, otherwise it will stay halted forever
}     
