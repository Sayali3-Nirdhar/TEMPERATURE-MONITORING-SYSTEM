# TEMPERATURE-MONITORING-SYSTEM

**company** = CODTECH IT SOLUTIONS

**NAME** = SAYALI SANTOSH NIRDHAR 

**INTERN ID** = CT08JED

**DOMAIN** = Embedded Systems 

**BATCH DURATION** = January 20th, 2025 to February 20th, 2025 

**MENTOR NAME** = Neela Santhosh 

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);

#define DHTPIN 2     
#define DHTTYPE DHT11 
DHT dht(DHTPIN, DHTTYPE);

void setup() {
    Serial.begin(9600);
    dht.begin();
    lcd.begin();
    lcd.backlight();
    lcd.setCursor(0, 0);
    lcd.print("Temp Monitor");
    delay(2000);
    lcd.clear();
}
void loop() {
    float temperature = dht.readTemperature();  
    float humidity = dht.readHumidity();     
    if (isnan(temperature) || isnan(humidity)) {
        Serial.println("Failed to read from DHT sensor!");
        lcd.setCursor(0, 0);
        lcd.print("Sensor Error");
        return;
    }
    lcd.setCursor(0, 0);
    lcd.print("Temp: ");
    lcd.print(temperature);
    lcd.print("C");
    lcd.setCursor(0, 1);
    lcd.print("Humid: ");
    lcd.print(humidity);
    lcd.print("%");
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println(" °C");
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.println(" %");
    delay(2000); // Update every 2 seconds
}
