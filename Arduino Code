const int ledPins[5] = {3, 5, 6, 9, 11}; // Blue, Green, Red, Yellow, White
const int buzzerPin = 2;


String inputString = "";
bool stringComplete = false;

void setup() {
  Serial.begin(9600);

 
  for (int i = 0; i < 5; i++) {
    pinMode(ledPins[i], OUTPUT);
    digitalWrite(ledPins[i], LOW);
  }


  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  
  while (Serial.available()) {
    char inChar = (char)Serial.read();
    if (inChar == '\n') {
      stringComplete = true;
      break;
    } else {
      inputString += inChar;
    }
  }

  if (stringComplete) {
    inputString.trim(); 

    
    if (inputString.startsWith("LED:")) {
      
      for (int i = 0; i < 5; i++) {
        digitalWrite(ledPins[i], LOW);
      }

      String ledList = inputString.substring(4);
      int index = 0;
      while (ledList.length() > 0) {
        int commaIndex = ledList.indexOf(',');
        String ledNum;
        if (commaIndex == -1) {
          ledNum = ledList;
          ledList = "";
        } else {
          ledNum = ledList.substring(0, commaIndex);
          ledList = ledList.substring(commaIndex + 1);
        }

        int ledIndex = ledNum.toInt() - 1; 
        if (ledIndex >= 0 && ledIndex < 5) {
          digitalWrite(ledPins[ledIndex], HIGH);
        }
      }
    }

    
    if (inputString.startsWith("NOTE:")) {
      String noteList = inputString.substring(5);
      int index = 0;
      while (noteList.length() > 0) {
        int commaIndex = noteList.indexOf(',');
        String noteStr;
        if (commaIndex == -1) {
          noteStr = noteList;
          noteList = "";
        } else {
          noteStr = noteList.substring(0, commaIndex);
          noteList = noteList.substring(commaIndex + 1);
        }

        int frequency = noteStr.toInt();
        if (frequency > 0) {
          tone(buzzerPin, frequency, 300); 
          delay(350); 
        }
      }
    }

    
    inputString = "";
    stringComplete = false;
  }
}
