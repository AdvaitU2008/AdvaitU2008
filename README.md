const int soundSensorAnalogPin = A1;
const int soundSensorDigitalPin = 2;
const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;

void setup() {
  pinMode(soundSensorAnalogPin, INPUT);
  pinMode(soundSensorDigitalPin, INPUT);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  int soundValue = analogRead(soundSensorAnalogPin);
  int digitalValue = digitalRead(soundSensorDigitalPin);

  // Map the sound value to the LED brightness (adjust these values as needed)
  int brightness = map(soundValue, 0, 1023, 0, 255);

  // Set the LED colors based on the sound level
  if (digitalValue == HIGH) {
    setColor(brightness, 0, 0); // Red component
  } else {
    setColor(0, 0, brightness); // Blue component
  }

  delay(20); // Adjust this delay to control the responsiveness
}

void setColor(int red, int green, int blue) {
  // Use 4-pin RGB LED strip with common anode configuration
  // Invert the values for common anode (HIGH means OFF, LOW means ON)
  analogWrite(redPin, 255 - red);
  analogWrite(greenPin, 255 - green);
  analogWrite(bluePin, 255 - blue);
}
