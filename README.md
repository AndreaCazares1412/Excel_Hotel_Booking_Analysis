# Hotel Booking Cancellation Analysis

### Objective
This analysis aims to explore hotel booking data, focusing on understanding cancellation rates, their impact on revenue, and key drivers for cancellations. The insights derived from this analysis are aimed at identifying strategies to minimize cancellations and improve revenue streams for the hotel.

### Questions to Analyze

1. What are the months with the highest average price and the highest number of bookings?
2. How do cancellations affect monthly revenue and loss percentages throughout the year?
3. How does reservation lead time affect booking status (cancelled vs. not cancelled)?
    3.1 How does lead time affect the probability of cancellation?
4. How does reservation room price affect booking status (cancelled vs. not cancelled)?
    4.1 How does room price influence the probability of cancellation?
5. How do cancellation rates differ between new and repeated guests?

### Excel Skills Used
The following Excel skills were utilized for analysis:

* 📊 Pivot Tables 
* 📈 Pivot Charts 
* 🧮 DAX (Data Analysis Expressions) 
* 🔍 Power Query 
* 💪 Power Pivot 

### Hotel Reservations Dataset
The dataset used for this project  is available via my Kaggle: [Hotel Reservations Dataset by Ahsan Raza](https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset). It includes detailed information on:

* 👨‍💼 Booking ID, date and status 
* 💰 Average Room Prices 
* 🏨 Room Type and Segment Type 
* 👥 Guests

## 1️⃣ What are the months with the highest average price and the highest number of bookings?

### 🔍 Skill: Power Query (ETL)

* 📥 Extract: I first used Power Query to extract the original data (Hotel_Bookings.xlsx), filtering for the year 2018 and selecting data with complete information, specifically filtering the stay_days column to exclude entries with 0 days.

* 🔄 Transform: Then, I transformed the query by changing column types, removing unnecessary columns, adding new columns relevant for the anlysis, cleaning text to eliminate specific words, and trimming excess whitespace.

📊 data_jobs_all
