# interfacing-ps2-remote
using bluetooth technology
code=
#include <PS2X_lib.h>
#define RELAY1  6                        

#define RELAY2  7                        

#define RELAY3  8                        

#define RELAY4  9

#define RELAY5  4                        

#define RELAY6  5



PS2X ps2x;
int error = 0;
byte vibrate = 0;

void setup() 
{
  Serial.begin(9600);
  error = ps2x.config_gamepad(3,12,A0,13,true,true);  //(CLOCK,COMMAND.ATTEN,DATA)

   if(error == 0)
   {
    Serial.print("Found Controller, configured successful ");
   }
   else
   {
    Serial.println("error came");
   }
   
  pinMode(RELAY1, OUTPUT);       

  pinMode(RELAY2, OUTPUT);

  pinMode(RELAY3, OUTPUT);

  pinMode(RELAY4, OUTPUT);

  PSB_PAD_DOWN = B;
  PSB_PAD_LEFT = L;
  PSB_PAD_RIGHT = R;
  PSB_BLUE = F;
} 

   void forward()
   {
    digitalWrite(RELAY1,HIGH);
    digitalWrite(RELAY2,LOW);
    digitalWrite(RELAY3,HIGH);
    digitalWrite(RELAY4,LOW);
   }

   void backward()
   {
    digitalWrite(RELAY1,LOW);
    digitalWrite(RELAY2,HIGH);
    digitalWrite(RELAY3,LOW);
    digitalWrite(RELAY4,HIGH);
   }

     void left()
   {
    digitalWrite(RELAY1,LOW);   //left motor//
    digitalWrite(RELAY2,HIGH);  //left motor//
    digitalWrite(RELAY3,HIGH);   //right motor//
    digitalWrite(RELAY4,LOW);  //right motor//
   }

      void RIGHT()
   {
    digitalWrite(RELAY1,HIGH);   //left motor//
    digitalWrite(RELAY2,LOW);  //left motor//
    digitalWrite(RELAY3,LOW);   //right motor//
    digitalWrite(RELAY4,HIGH);  //right motor//
   }

  void cylinder_ON()
  {
    while(1)
    {
    digitalWrite(RELAY5,HIGH);
    digitalWrite(RELAY6,LOW);
    }
  }
  

void loop()
{
  int temp = Serial.read(ps2x.Button());
  ps2x.read_gamepad(false,vibrate);

 
 switch(temp)
 {
  case 'F' : forward(); break;
  case 'L' : left(); break;
  case 'R' : right(); break;
  case 'B' : backward(); break;

  default : break;
 }
}
