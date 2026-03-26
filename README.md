# Flight Delay Prediction

This project analyzes U.S. domestic flight data to predict both the likelihood and magnitude of flight delays using historical operational data.

## Overview

Flight delays remain a major operational challenge in the airline industry:

* Only **70–80% of flights arrive on time**
* **20–30% are delayed** by 15 minutes or more

The primary causes of delays include:

* Late aircraft (~40%)
* Carrier-related issues (~30%)

Improving delay prediction can help airlines optimize operations and provide better information to passengers.

## Research Questions

1. Can we predict whether a flight will be delayed?
2. Can we predict the magnitude of the delay?

## Data

* **Source:** Bureau of Transportation Statistics – Marketing Carrier On-Time Performance
* **Link:** https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FGK&QO_fu146_anzr=b0-gvzr
* **Time Period:** January 2018 – November 2025
* **Size:** ~30 million records
* **Unit of Analysis:** Individual domestic flight

## Features

### Core Variable Groups

* **Flight Identifiers:** Carrier, origin, destination, date
* **Performance Metrics:**
  * Scheduled vs. actual departure/arrival
  * Delay in minutes
  * Binary indicator (15+ minute delay)
* **Flight Status:** Cancellation and diversion indicators with reason codes
* **Delay Causes:**
  * Carrier
  * Weather
  * National Airspace System (NAS)
  * Security
  * Late aircraft
* **Operational Metrics:**
  * Air time
  * Elapsed time
  * Taxi in/out
  * Distance

## Data Preparation & Feature Engineering

No missing values were present, allowing full focus on feature engineering.

### Temporal Features

* Year, month, day
* Day of week
* Weekend indicator

### Time Features

* Converted HHMM format to minutes since midnight
* Extracted:

  * Departure hour
  * Arrival hour
  * Time-of-day categories (night, morning, afternoon, evening)
  * Rush hour indicator

### Route & Airline Features

* Route (origin → destination)
* Airline label encoding
* Route frequency counts

### Cyclical Encoding

* Sine/cosine transformations for:

  * Hour of day
  * Day of week

### Operational Features

* Departure delay ratio
* Delay recovery indicator
* Late departure flag
* Total taxi time
* Taxi time ratio
* Weather delay indicator

### Historical Aggregates

* Average delays by:

  * Origin airport
  * Destination airport
  * Airline
  * Route
* Airport traffic volume
* Origin × hour average delay
* Seasonal peak indicators

## Modeling Approach

Two prediction tasks were developed:

* **Classification:** Predict whether a flight is delayed (15+ minutes)
* **Regression:** Predict total delay time (in minutes)

Models can include:

* Logistic Regression
* Tree-based methods (Random Forest, Gradient Boosting)
* Regularized models

## Use Cases

* Airline operational planning
* Delay risk estimation for passengers
* Scheduling and routing optimization
* Early warning systems for disruptions

## Limitations

* Historical data may not fully capture real-time disruptions
* External shocks (e.g., extreme weather, system outages) are difficult to predict
* Model performance may vary across airports and airlines
* Data includes COVID-19 pandemic period in which there was a significant decrease in the volume of flights

## Future Work

* Incorporate real-time weather and air traffic data
* Filter out COVID-19 pandemic years
* Apply advanced models (e.g. neural networks)
* Build a live delay prediction dashboard
* Extend analysis to international flights
