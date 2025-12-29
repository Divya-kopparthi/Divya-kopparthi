// Distance Meter Project using Ultrasonic Sensor HC-SR04
#define TRIG_PIN 8   // Trigger connected to D8
#define ECHO_PIN 9   // Echo connected to D9

void setup() {
  Serial.begin(9600);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  Serial.println("Distance Meter Initialized");
}

void loop() {
  // Send ultrasonic pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Measure response time
  long duration = pulseIn(ECHO_PIN, HIGH, 30000); // Timeout after 30ms (max range ~5m)
  float distance = duration * 0.0343 / 2; // Convert to cm

  if (duration == 0) {
    Serial.println("Out of range or no object detected");
  } else {
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");
  }

  delay(1000);
}
