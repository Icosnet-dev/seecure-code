#include <Wire.h>

#include "SparkFunBME280.h"
BME280 mySensorA; //Uses default I2C address 0x77
BME280 mySensorB; //Uses I2C address 0x76 (jumper closed)

void setup()
{
  Serial.begin(9600);
  Serial.println("Example showing alternate I2C addresses");

  Wire.begin();

  mySensorA.setI2CAddress(0x77); //The default for the SparkFun Environmental Combo board is 0x77 (jumper open).
  //If you close the jumper it is 0x76
  //The I2C address must be set before .begin() otherwise the cal values will fail to load.

  if(mySensorA.beginI2C() == false) Serial.println("Sensor A connect failed");

  mySensorB.setI2CAddress(0x76); //Connect to a second sensor
  if(mySensorB.beginI2C() == false) Serial.println("Sensor B connect failed");
}

void loop()
{
  Serial.print("HumidityA: ");
  Serial.print(mySensorA.readFloatHumidity(), 0);

  Serial.print(" PressureA: ");
  Serial.print(mySensorA.readFloatPressure(), 0);

  Serial.print(" TempA: ");
  //Serial.print(mySensorA.readTempC(), 2);
  Serial.print(mySensorA.readTempF(), 2);

  Serial.print(" HumidityB: ");
  Serial.print(mySensorB.readFloatHumidity(), 0);

  Serial.print(" PressureB: ");
  Serial.print(mySensorB.readFloatPressure(), 0);

  Serial.print(" TempB: ");
  //Serial.print(mySensorB.readTempC(), 2);
  Serial.print(mySensorB.readTempF(), 2);

  Serial.println();

  delay(50);
}
