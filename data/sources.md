# IoT Sensor Data & System Resources

## Primary Data Sources

### IoT Sensors

**Soil Moisture Sensor**
- **Model**: Capacitive Soil Moisture Sensor
- **Range**: 0-1023 (ADC value)
- **Calibration**: 0% (dry) ~ 100% (saturated)
- **Measurement Interval**: 5 minutes
- **Unit**: Volumetric Water Content (%)

**Temperature & Humidity Sensor**
- **Model**: DHT22 (or BME280)
- **Temperature Range**: -40°C to 80°C (±0.5°C accuracy)
- **Humidity Range**: 0-100% RH (±2% accuracy)
- **Measurement Interval**: 5 minutes
- **Output**: Digital (I2C or OneWire)

**Light Intensity Sensor**
- **Model**: LDR or BH1750 Digital Sensor
- **Range**: 0-65535 (0-100,000 lux)
- **Measurement Interval**: 10 minutes
- **Purpose**: Track natural light for photosynthesis

**pH Sensor** (Optional)
- **Range**: 0-14 pH units
- **Accuracy**: ±0.1 pH
- **Measurement Interval**: Hourly

### Data Collection Hardware

**Microcontroller**: Arduino/ESP32/Raspberry Pi
- **Sampling Rate**: All sensors @ 300s intervals
- **Storage**: Local SD card + cloud sync
- **Connectivity**: WiFi (ESP32) or wired (Pi)
- **Power**: Solar-powered (optional)

**Database Backend**: MongoDB / PostgreSQL
- **Storage Format**: Time-series collections
- **Retention Period**: 12 months rolling
- **Sync Frequency**: Real-time (WiFi-enabled)

---

## Data Dictionary

### Sensor Readings Table

| Field | Type | Range | Description |
|-------|------|-------|-------------|
| timestamp | DateTime | ISO 8601 | UTC time of measurement |
| sensor_id | String | Garden-001 to 999 | Unique sensor identifier |
| soil_moisture | Float | 0-100 | % volumetric water content |
| temperature | Float | -40 to 80 | °C |
| humidity | Float | 0-100 | % relative humidity |
| light_intensity | Integer | 0-65535 | Lux (or ADC value) |
| ph_value | Float | 0-14 | pH units (optional) |
| battery_level | Float | 0-100 | % battery remaining (wireless) |
| signal_strength | Integer | -120 to -30 | dBm (signal quality) |

### Plant Configuration Table

| Field | Type | Description |
|-------|------|-------------|
| plant_id | String | Unique plant identifier |
| plant_name | String | Common/scientific name |
| plant_type | Categorical | Vegetable, Herb, Ornamental, etc. |
| irrigation_threshold | Float | Min soil moisture % for watering |
| optimal_temp_min | Float | Preferred minimum temperature (°C) |
| optimal_temp_max | Float | Preferred maximum temperature (°C) |
| optimal_humidity_min | Float | Preferred minimum humidity (%) |
| optimal_humidity_max | Float | Preferred maximum humidity (%) |
| watering_duration | Integer | Duration of irrigation in seconds |
| care_notes | String | Special care instructions |

---

## Data Quality & Constraints

### Sensor Accuracy

| Sensor | Accuracy | Drift Rate | Calibration Interval |
|--------|----------|------------|---------------------|
| Soil Moisture | ±5% | 2-3% per month | Monthly |
| Temperature | ±0.5°C | Minimal | Every 6 months |
| Humidity | ±2% | 0.5% per month | Quarterly |
| Light Intensity | ±3% | Minimal | Yearly |

### Known Issues & Mitigation

| Issue | Impact | Solution |
|-------|--------|----------|
| Sensor saturation | False high moisture readings | Implement max threshold check |
| Temperature hysteresis | Delayed readings | Use smoothing filter (moving average) |
| Light sensor noise | Erratic readings | Apply low-pass filter (5-min average) |
| WiFi dropouts | Missing data points | Store locally, sync when reconnected |
| Power failures | Data loss during outages | Add backup battery (UPS) |
| Sensor drift | Measurement errors over time | Implement calibration reminders |

### Data Collection Gap Handling
- **< 5 mins**: Interpolation (linear)
- **5-30 mins**: Forward-fill (last known value)
- **> 30 mins**: Mark as missing, alert user
- **> 24 hrs**: Log as sensor failure

---

## Data Acquisition Pipeline

### Step-by-Step Process
1. **Sensor Reading**: Microcontroller polls all sensors every 5 minutes
2. **Data Validation**: Check if readings within expected range
3. **Local Storage**: Save to SD card/local database
4. **Cloud Sync**: Upload to cloud database (if connected)
5. **Processing**: Calculate irrigation needs
6. **Action**: Trigger watering if threshold exceeded
7. **Logging**: Record all actions with timestamps

### Data Validation Rules
```python
soil_moisture: 0 <= value <= 100
temperature: -40 <= value <= 80
humidity: 0 <= value <= 100
light_intensity: 0 <= value <= 100000
```

---

## Plant Database Reference

### Common Plants & Thresholds

**Tomato**
- Soil Moisture: 60-80%
- Temperature: 20-25°C
- Humidity: 50-70%
- Watering: 1-2 L every 2-3 days

**Lettuce**
- Soil Moisture: 70-80%
- Temperature: 15-20°C
- Humidity: 60-80%
- Watering: Keep consistently moist

**Basil**
- Soil Moisture: 50-70%
- Temperature: 18-25°C
- Humidity: 50-60%
- Watering: Let dry slightly between waterings

**Roses**
- Soil Moisture: 60-75%
- Temperature: 15-22°C
- Humidity: 40-60%
- Watering: Deep, infrequent watering

---

## System Architecture

### Data Flow
```
IoT Sensors
    ↓
[Microcontroller] → [Local Database]
    ↓
[WiFi/Ethernet]
    ↓
[Cloud DB (MongoDB/PostgreSQL)]
    ↓
[Analytics Engine] → [Predictions]
    ↓
[Irrigation Controller] → [Solenoid Valve]
```

---

## Environmental Factors

### Seasonal Adjustments
- **Spring (Mar-May)**: Increase watering, monitor frost
- **Summer (Jun-Aug)**: Reduce manual watering, shade plants
- **Fall (Sep-Nov)**: Decrease watering, harvest preparation
- **Winter (Dec-Feb)**: Minimal watering, freeze protection

### Weather Integration
- API: OpenWeather forecast
- Purpose: Adjust irrigation based on predicted rainfall
- Logic: Skip watering if rain expected within 24 hours

---

## Reproducibility & Setup

### Hardware Setup
1. Connect soil moisture sensor to analog pin A0
2. Connect DHT22 to digital pin D5
3. Connect light sensor to A1
4. Configure WiFi credentials in `config.py`
5. Run `calibration_routine.py` before first use

### Data Export
- **Format**: CSV, JSON
- **Frequency**: Daily, weekly, monthly snapshots
- **Location**: `/data/exports/`

### Calibration
```bash
# Run calibration wizard
python calibrate_sensors.py

# Test connection
python test_sensors.py
```

**Last Updated**: November 2025  
**Data Version**: v1.0  
**Hardware Version**: v2.1
