# Medicine-Dispenser
#include <LiquidCrystal_I2C.h>
#include <Servo.h>
#include <Keypad.h>


LiquidCrystal_I2C lcd(0x3F, 2, 1, 0, 4,5,6,7);

Servo servo1;
Servo servo2;
Servo servo3;


const byte numRows =4;
const byte numCols =4;

char keyMap[numRows][numCols] = {
  {'1', '2', '3', 'A'},
  {'4', '5', '6', 'B'},
  {'7', '8', '9', 'C'},
  {'*', '0', '#', 'D'}};

byte rowPins[numRows] = {12, 8, 7,6};
byte colPins[numCols] = {5, 4,3,2};


int serv1 = 9;
int serv2 = 10;
int serv3 = 11;

#define led A1

//#define buz A0

Keypad myKeypad = Keypad(makeKeymap(keyMap), rowPins, colPins, numRows, numCols);

class Flasher
{
  //class member variables initialized at startup
  public:
  int ledPin;
  long onTime; //milli seconds of on time
  long offTime; //milli seconds of off time

  int ledState;
  unsigned long previousMillis;

  public:
  Flasher(int pin, long on, long off)
  {
    ledPin = pin;
    pinMode(ledPin, OUTPUT);

    onTime = on;
    offTime = off;

    ledState = LOW;
    previousMillis = 0;
  }

  void Update()
  {
    unsigned long currentMillis = millis();

    if((ledState == HIGH) && (currentMillis - previousMillis >= onTime))
    {
      ledState = LOW;
      previousMillis = currentMillis;
      digitalWrite(ledPin, ledState);
    }
    else if((ledState == LOW) &&(currentMillis - previousMillis >= offTime))
    {
      ledState = HIGH;
      previousMillis = currentMillis;
      digitalWrite(ledPin, ledState);
    }
  }
};

Flasher buzzer(13, 14, 14);
void setup() {
  // put your setup code here, to run once:
  pinMode(led, OUTPUT);
 // pinMode(buz, OUTPUT);
  servo1.attach(serv1);
  servo2.attach(serv2);
  servo3.attach(serv3);

  lcd.begin(20, 4);
  lcd.setBacklightPin(3, POSITIVE);
  lcd.setBacklight(HIGH);
  lcd.setCursor(0,0);
  lcd.print("Automated Medicine");
  lcd.setCursor(0,1);
  lcd.print("Dispenser by");
  lcd.setCursor(0,2);
  lcd.print("RAJI, Aisha O.");
  lcd.setCursor(0,3);
  lcd.print("13/30GP014");
  delay(5000);
//  digitalWrite(buzzer.ledPin, HIGH);
  //delay(5000);
  //digitalWrite(buzzer.ledPin, LOW);
}

void loop() {
  // put your main code here, to run repeatedly:
//    if(digitalRead(17)== HIGH)
//    {
//      buzzer.Update();
//    }
    drug1();
}

void buzz()
{
}

void drug1()
{
  //analogWrite(buz, 20);
  //delay(20);
  //analogWrite(buz, 0);
  digitalWrite(led, HIGH);
  delay(1000);
  //digitalWrite(led, LOW);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("How many tablets do");
  lcd.setCursor(0,1);
  lcd.print("you want to take");
  
  char keyPressed = myKeypad.getKey();
 
  if(keyPressed != NO_KEY)
  {
    lcd.clear();
   // lcd.print(keyPressed);
    delay(2);
    //digitalWrite(led, HIGH);
    delay(2);
    switch(keyPressed)
    {
      case '1':
      lcd.print("1 pill: From storage 1");
      digitalWrite(led, HIGH);
      delay(50);
      for(int pos = 0; pos <= 90; pos++)
      {
        servo1.write(pos);
        delay(15);
      }
      for(int
      pos = 90; pos >= 0; pos--)
      {
        servo1.write(pos);
        delay(15);
        digitalWrite(led, LOW);
     }
      delay(10);
      digitalWrite(led, LOW);
      delay(10);
     
      break;

      case '2':
      lcd.print("2 pills: From storage 1");
      for(int num = 0; num < 2; num++)
      
      {
        digitalWrite(led, HIGH);
        delay(50);
        for(int pos = 0; pos <= 90; pos++)
        {
          servo1.write(pos);
          delay(15);
        }
        digitalWrite(led, LOW);
        delay(5);
        for(int pos = 90; pos >= 0; pos --)
        {
          servo1.write(pos);
          delay(15);
        }
      }
      break;
      
      
      case '3':
      lcd.print("3 pills: From Storage 1");
      for(int bos = 0; bos <3; bos++)
      {
        digitalWrite(led, HIGH);
        delay(50);
        for (int pos = 0; pos <= 90; pos++)
        {
          servo1.write(pos);
          delay(15);
        }
        digitalWrite(led, LOW);
        delay(5);
        for (int pos = 90; pos >= 0; pos --)
        {
          servo1.write(pos);
          delay(15); 
        }
      }
      break;
      
      case '4':
      lcd.print("1 pill: From storage 2");
      digitalWrite(led, HIGH);
      delay(50);
      for(int pos = 0; pos <= 90; pos++)
      {
        servo2.write(pos);
        delay(15);
      }
      for(int pos = 90; pos >= 0; pos--)
      {
        servo2.write(pos);
        delay(15);
        digitalWrite(led, LOW);
     }
      delay(10);
      digitalWrite(led, LOW);
      delay(10);
     
      break;

      case '5':
      lcd.print("2 pills: From storage 2");
      for(int num = 0; num < 2; num++)
      {
        digitalWrite(led, HIGH);
        delay(50);
        for(int pos = 0; pos <= 90; pos++)
        {
          servo2.write(pos);
          delay(15);
        }
        digitalWrite(led, LOW);
        delay(5);
        for(int pos = 90; pos >= 0; pos --)
        {
          servo2.write(pos);
          delay(15);
        }
      }
      break;
            
      case '6':
      lcd.print("3 pills: From storage 2");
      for(int bos = 0; bos <3; bos++)
      {
        digitalWrite(led, HIGH);
        delay(50);
        for (int pos = 0; pos <= 90; pos++)
        {
          servo2.write(pos);
          delay(15);
        }
        digitalWrite(led, LOW);
        delay(5);
        for (int pos = 90; pos >= 0; pos --)
        {
          servo2.write(pos);
          delay(15); 
        }
      }
      break;

      case '7':
      lcd.print("1 pill: From storage 3");
      digitalWrite(led, HIGH);
      delay(50);
      for(int pos = 0; pos <= 110; pos++)
      {
        servo3.write(pos);
        delay(10);
      }
      for(int pos = 110; pos >= 0; pos--)
      {
        servo3.write(pos);
        delay(15);
        digitalWrite(led, LOW);
     }
      delay(10);
      digitalWrite(led, LOW);
      delay(10);
     
      break;

      case '8':
      lcd.print("2 pills: From storage 3");
      for(int num = 0; num < 2; num++)
      {
        digitalWrite(led, HIGH);
        delay(50);
        for(int pos = 0; pos <= 110; pos++)
        {
          servo3.write(pos);
          delay(10);
        }
        digitalWrite(led, LOW);
        delay(5);
        for(int pos = 110; pos >= 0; pos --)
        {
          servo3.write(pos);
          delay(15);
        }
      }
      break;
      
      
      case '9':
      lcd.print("3 pills: From storage 3");
      for(int bos = 0; bos <3; bos++)
      {
        digitalWrite(led, HIGH);
        delay(50);
        for (int pos = 0; pos <= 110; pos++)
        {
          servo3.write(pos);
          delay(10);
        }
        digitalWrite(led, LOW);
        delay(5);
        for (int pos = 110; pos >= 0; pos --)
        {
          servo3.write(pos);
          delay(15); 
        }
      }
      break;

      default:
      digitalWrite(led, HIGH);
      break;
     }
     //digitalWrite(led, LOW);
  }
  //digitalWrite(led, LOW);
}

//void drug2()
//{
//  //analogWrite(buz, 20);
//  //delay(20);
//  //analogWrite(buz, 0);
//  digitalWrite(led, HIGH);
//  delay(1000);
//  //digitalWrite(led, LOW);
//  lcd.clear();
//  lcd.setCursor(0,0);
//  lcd.print("How many tablets do");
//  lcd.setCursor(0,1);
//  lcd.print("you want to take");
//  
//  char keyPressed = myKeypad.getKey();
// 
//
//  if(keyPressed != NO_KEY)
//  {
//    lcd.clear();
//    lcd.print(keyPressed);
//    delay(2);
//    //digitalWrite(led, HIGH);
//    delay(2);
//    switch(keyPressed)
//    {
//      case '1':
//      digitalWrite(led, HIGH);
//      delay(50);
//      for(int pos = 0; pos <= 90; pos++)
//      {
//        servo2.write(pos);
//        delay(15);
//      }
//      for(int
//      pos = 90; pos >= 0; pos--)
//      {
//        servo2.write(pos);
//        delay(15);
//        digitalWrite(led, LOW);
//     }
//      delay(10);
//      digitalWrite(led, LOW);
//      delay(10);
//     
//      break;
//
//      case '2':
//      for(int num = 0; num < 2; num++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for(int pos = 0; pos <= 90; pos++)
//        {
//          servo2.write(pos);
//          delay(15);
//        }
//        digitalWrite(led, LOW);
//        delay(5);
//        for(int pos = 90; pos >= 0; pos --)
//        {
//          servo2.write(pos);
//          delay(15);
//        }
//      }
//      break;
//      
//      
//      case '3':
//      for(int bos = 0; bos <3; bos++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for (int pos = 0; pos <= 90; pos++)
//        {
//          servo2.write(pos);
//          delay(15);
//        }
//        digitalWrite(led, LOW);
//        delay(5);
//        for (int pos = 90; pos >= 0; pos --)
//        {
//          servo2.write(pos);
//          delay(15); 
//        }
//      }
//      break;
//      
//      case '4':
//      for (int csi = 0; csi <4; csi++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for (int pos = 0; pos <=90; pos++)
//        {
//          servo2.write(pos);
//          delay(15);
//        }
//        delay(5);
//        digitalWrite(led, LOW);
//        for (int pos = 90; pos >= 0; pos--) 
//        {
//          servo2.write(pos);
//          delay(15);
//          
//        }
//      }
//      break;
//
//      default:
//      digitalWrite(led, HIGH);
//      break;
//     }
//     //digitalWrite(led, LOW);
//  }
//  //digitalWrite(led, LOW);
//}
//
//void drug3()
//{
//  //analogWrite(buz, 20);
//  //delay(20);
//  //analogWrite(buz, 0);
//  digitalWrite(led, HIGH);
//  delay(1000);
//  //digitalWrite(led, LOW);
//  lcd.clear();
//  lcd.setCursor(0,0);
//  lcd.print("How many tablets do");
//  lcd.setCursor(0,1);
//  lcd.print("you want to take");
//  
//  char keyPressed = myKeypad.getKey();
// 
//
//  if(keyPressed != NO_KEY)
//  {
//    lcd.clear();
//    lcd.print(keyPressed);
//    delay(2);
//    //digitalWrite(led, HIGH);
//    delay(2);
//    switch(keyPressed)
//    {
//      case '1':
//      digitalWrite(led, HIGH);
//      delay(50);
//      for(int pos = 0; pos <= 90; pos++)
//      {
//        servo3.write(pos);
//        delay(15);
//      }
//      for(int
//      pos = 90; pos >= 0; pos--)
//      {
//        servo3.write(pos);
//        delay(15);
//        digitalWrite(led, LOW);
//     }
//      delay(10);
//      digitalWrite(led, LOW);
//      delay(10);
//     
//      break;
//
//      case '2':
//      for(int num = 0; num < 2; num++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for(int pos = 0; pos <= 90; pos++)
//        {
//          servo3.write(pos);
//          delay(15);
//        }
//        digitalWrite(led, LOW);
//        delay(5);
//        for(int pos = 90; pos >= 0; pos --)
//        {
//          servo3.write(pos);
//          delay(15);
//        }
//      }
//      break;
//         case '3':
//      for(int bos = 0; bos <3; bos++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for (int pos = 0; pos <= 90; pos++)
//        {
//          servo3.write(pos);
//          delay(15);
//        }
//        digitalWrite(led, LOW);
//        delay(5);
//        for (int pos = 90; pos >= 0; pos --)
//        {
//          servo3.write(pos);
//          delay(15); 
//        }
//      }
//      break;
//      
//      case '4':
//      for (int csi = 0; csi <4; csi++)
//      {
//        digitalWrite(led, HIGH);
//        delay(50);
//        for (int pos = 0; pos <=90; pos++)
//        {
//          servo3.write(pos);
//          delay(15);
//        }
//        delay(5);
//        digitalWrite(led, LOW);
//        for (int pos = 90; pos >= 0; pos--) 
//        {
//          servo3.write(pos);
//          delay(15);
//              }
//      }
//      break;
//
//      default:
//      digitalWrite(led, HIGH);
//      break;
//     }
//     //digitalWrite(led, LOW);
//  }
//  //digitalWrite(led, LOW);
//}
