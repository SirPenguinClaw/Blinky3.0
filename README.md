# Blinky3.0
Blinks. Just blinks. Nothing more. Nothing less. Interesting huh?


//GOAL: Make a SEVEN SEGMENT COUNTER (counts from 0 up to 9)

/*
 * HOW TO SHIFT NUMBERS IN C
 * 00111000 >> 1 = 00011100
 * 00111000 >> 2 = 00001110
 * x%2 = true if x is odd -OR- x%2 = false (least sig. bit is 0)
 * 
 * 
 * refactor to output a byte at a time
 * write a function that accepts a uint8_t input that outputs the corresponding leds on the 7 seg display, hint switch
 * debug (try not to cry)
 */



//All numbers = GPIO - General Purpose Input Output
#define SRCLK 4
#define SRCLR 16
#define RCLK 17
#define OE 5
#define SER 18
#define SPEED 1000
#define SERHIGH digitalWrite(SER, HIGH)
#define SERLOW digitalWrite(SER, LOW)



void setup() {
  // put your setup code here, to run once:
  pinMode(SRCLK, OUTPUT);
  pinMode(SRCLR, OUTPUT);
  pinMode(RCLK, OUTPUT);
  pinMode(OE, OUTPUT);
  pinMode(SER, OUTPUT);

  //Set OE to low to enable output
  digitalWrite(OE, LOW);
  //Set SRCLR to high to disable clear
  digitalWrite(SRCLR, HIGH);


  //Set all bits to LOW (0)
  for (int i = 0; i < 8; i++) {
    outputBit(false);
  }

  //Set counter to 0
  uint16_t counter = 0;

}



void loop() {
  // put your main code here, to run repeatedly:
  
  for (uint16_t i = 0; i <= 9; i++) {   // Loops from 0-9
    for (uint8_t l = 0; l < 8; l++) {   // Loops from 0-7, sets up LEDs to be latched

      //If statements that checks for what number counter is on, and displays it
      //  also increases counter by 1 once finished
      // 0 = 1111110
        if (counter = 0) {
          //Logic
          for (int i = 0; i < 6; i++) {
            outputBit(true);
          }
            outputBit(false);
  
          counter++;
        }

      // 1 = 0110000
        if (counter = 1) {
          //Logic
            outputBit(false);
            outputBit(true);
            outputBit(true);
          for (int i = 0; i < 5; i++) {
            outputBit(false);
          }
  
          counter++;
        }
      
      // 2 = 1101101
        if (counter = 2) {
          //Logic
            outputBit(true);
            outputBit(true);
            outputBit(false);
            outputBit(true);
            outputBit(true);
            outputBit(false);
            outputBit(true);
  
          counter++;
        }

      // 3 = 1111001
        if (counter = 3) {
          //Logic
          for (int i = 0; i < 4; i++) {
            outputBit(true);
          }
            outputBit(false);
            outputBit(false);
            outputBit(true);
  
          counter++;
        }
      
      // 4 = 0110011
        if (counter = 4) {
          //Logic
            outputBit(false);
            outputBit(true);
            outputBit(true);
            outputBit(false);
            outputBit(false);
            outputBit(true);
            outputBit(true);
  
          counter++;
        }
      
      // 5 = 1011011
        if (counter = 5) {
          //Logic
            outputBit(true);
            outputBit(false);
            outputBit(true);
            outputBit(true);
            outputBit(false);
            outputBit(true);
            outputBit(true);
  
          counter++;
        }
      
      // 6 = 1011111
        if (counter = 6) {
          //Logic
            outputBit(true);
            outputBit(false);
          for (int i = 0; i < 5; i++) {
            outputBit(true);
          }
  
          counter++;
        }
      
      // 7 = 1110000
        if (counter = 7) {
          //Logic
          for (int i = 0; i < 3; i++) {
            outputBit(true);
          }
          for (int i = 0; i < 4; i++) {
            outputBit(false);
          }
  
          counter++;
        }

      // 8 = 1111111
        if (counter = 8) {
          //Logic
          for (int i = 0; i < 7; i++) {
            outputBit(true);
          }
          
          counter++; 
        }

      // 9 = 1110011
        if (counter = 9) {    // 9 = 1110011
          //Logic
          for (int i = 0; i < 3; i++) {
            outputBit(true);
          }
            outputBit(false);
            outputBit(false);
            outputBit(true);
            outputBit(true);
  
          counter = 0;
        }
    
    clockLatch();
    delay(SPEED);
    }
  }
}



//Functions
void clockSR (){  //SRCLK 
    digitalWrite(SRCLK, HIGH);
    delay(1);
    digitalWrite(SRCLK, LOW);
    delay(1);
}

void clockLatch(){  //RCLK
    digitalWrite(RCLK, HIGH);
    delay(1);
    digitalWrite(RCLK, LOW);
    delay(1);
}

void outputBit(uint8_t x){   //sends the bit output
    if (x) {                 // If x is HIGH
      SERHIGH;               // Display HIGH
      clockSR();             // Shift to next bit
    } else {                 // Otherwise
      SERLOW;                // Display LOW
      clockSR();             // Shift to next bit
    }
}
