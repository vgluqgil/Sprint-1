#include <Wire.h>
#include <Adafruit_ADS1X15.h>

Adafruit_ADS1115 ads;
#define channelValue 0
#define offset 0.73
#define samplingInterval 20
#define printInterval 800
#define ArrayLength 40
int pHArray[ArrayLength];
int pHArrayIndex = 0;

float AverageSample(int numSamples, int* samples) {
  long sum = 0;

  for (int i = 0; i < numSamples; ++i) {
    sum += samples[i];
  }

  return static_cast<float>(sum) / numSamples;
}

void setup() {
  Serial.begin(9600);
  Serial.println(" Inicializando el medidor de ph");
  ads.begin();
  ads.setGain(GAIN_ONE);
}

void loop() {
  static unsigned long samplingTime = millis();
  static unsigned long printTime = millis();
  static float pHValue, voltage;

  if (millis() - samplingTime > samplingInterval) {
    pHArray[pHArrayIndex++] = ads.readADC_SingleEnded(0);
    if (pHArrayIndex == ArrayLength) pHArrayIndex = 0;
    voltage = pHArray[pHArrayIndex] * 4.096 / (pow(2, 15) - 1);
    pHValue = 3.5 * voltage + offset;
    samplingTime = millis();
  }

  if (millis() - printTime > printInterval) {
    float averagedVoltage = AverageSample(ArrayLength, pHArray);
    
    Serial.print("Average voltage: ");
    Serial.print(averagedVoltage, 2);

    float averagedpH = 3.5 * averagedVoltage + offset;
    Serial.print("  pH value: ");
    Serial.println(averagedpH, 2);

    printTime =millis();
}

if (millis() - printTime > printInterval) {
    float averagedVoltage = AverageSample(ArrayLength, pHArray);
    
    Serial.print("Average voltage: ");
    Serial.print(averagedVoltage, 2);

    float averagedpH = 3.5 * averagedVoltage + offset;
    Serial.print("  pH value: ");
    Serial.println(averagedpH, 2);

    printTime =millis();
}
}
