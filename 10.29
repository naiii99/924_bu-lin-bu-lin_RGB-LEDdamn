const int rledPin = 8 ;
const int gledPin = 9 ;
const int bledPin = 10 ;
const int buttonPin = 7;
int mood = 0 ;
const int neutralMood = 10 ;
int buttonState = 0;
bool buttonPressed = false;
unsigned long touchedTimer = 0;
unsigned long reducedTimer = 0;
const long unTouchInterval = 5000;
const long reducedInterval = 1000;

void setup(){
  pinMode(buttonPin,INPUT);
  pinMode(rledPin,OUTPUT);
  pinMode(gledPin,OUTPUT);
  pinMode(bledPin,OUTPUT);

  mood = neutralMood;
}
void loop(){
  showLEDState(mood);

  buttonState = digitalRead(buttonPin);

  if(buttonState == HIGH && !buttonPressed){
    mood = mood + 1 ;
    if(mood > 20) mood = 20;
    touchedTimer = millis();
    buttonPressed = true;
  }
  if(buttonState == LOW && buttonPressed){
    buttonPressed = false;
  }
  unsigned long currentTimer = millis();
  if(currentTimer - touchedTimer > unTouchInterval){
    if(currentTimer - reducedTimer > reducedInterval){
      mood = mood - 1;
      if(mood < 0) mood = 0;
      reducedTimer = currentTimer;
    }
  }
}
void showLEDState(int state){
  float brightnessInterval = 255/10.0;
  if(state >= neutralMood){
    analogWrite(rledPin , 255);
    analogWrite(gledPin , brightnessInterval * (state - neutralMood));
    analogWrite(bledPin , 255 -brightnessInterval * (state - neutralMood));
  }
  else{
    analogWrite(bledPin , 255);
    analogWrite(gledPin , brightnessInterval * (neutralMood - state));
    analogWrite(rledPin , 255 - brightnessInterval * (neutralMood - state));
  }
}
