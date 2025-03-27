# Hotel Booking Cancellation Analysis

### Objective
This analysis aims to explore hotel booking data, focusing on understanding cancellation rates, their impact on revenue, and key drivers for cancellations. The insights derived from this analysis are aimed at identifying strategies to minimize cancellations and improve revenue streams for the hotel.

### Questions to Analyze

1. What are the months with the highest average price and the highest number of bookings?
2. How do cancellations impact monthly revenue and the percentage of revenue lost throughout the year?
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

## 🔍 Power Query (ETL) and DAX Integration: Data Extraction, Transformation, and Analysis

📥 **Extract**: I first used Power Query to extract the original data (Hotel_Bookings.xlsx), filtering for the year 2018 and selecting data with complete information, specifically filtering the stay_days column to exclude entries with 0 days, as these were not logical. This ensured that the data I worked with was relevant and accurate.

🔄 **Transform**: After extracting the data, I transformed the query by adjusting column types, removing unnecessary columns, and adding new ones relevant for analysis. I also cleaned the text by removing specific unwanted words and trimming excess whitespace. This helped to standardize the dataset and improve its usability for analysis.

📊 Reservations_Stay_Days

![Texto alternativo](hotel_analysis_images/tranformation_power_query.png)

🔗 **Load**: Finally, I loaded both transformed queries into the workbook, setting the foundation for my subsequent analysis.

🔀 **Integrating Power Query with Power Pivot for DAX Calculations**: To further enhance the analysis, I connected the transformed data in Power Query to Power Pivot, enabling advanced calculations using DAX. This allowed me to create powerful metrics, aggregations, and pivot tables to gain deeper insights into the hotel bookings data.

![Texto alternativo](hotel_analysis_images/conection_power_pivot.png)

  
## 📊Analysis

### 1️⃣ What are the months with the highest average price and the highest number of bookings?

### 📈Pivot Table
* 📊 I moved the month_name to the rows area, total_reservations and median_price_room into the values area.

### 🧮 DAX
To calculate the median_price_room each month I used DAX.

```
Median Price Room := MEDIAN(Reservation_Stay_Days[avg_price_per_room])
```

### 💡 Insights
* October has the highest number of bookings, with more than 3,300 reservations, indicating peak demand during this month.
* June follows closely with a median price of 115€,  indicating a strong season but with a slightly lower average price compared to September.
* September has the highest median room price, at 119€ which is higher than the other months.

![Texto alternativo](hotel_analysis_images/1.png)

### 🤔 So What
* **October** leads in bookings, while September sees the highest room prices, indicating different strategies for peak seasons. October likely represents the volume-driven peak, while September may focus on higher-value bookings.

### 2️⃣ How do cancellations impact monthly revenue and the percentage of revenue lost throughout the year?

### 📈Pivot Table
* 📊 I moved the booking_status (Canceled and Not Canceled) and month_name to the rows area, and the total_revenue into the values area.

### 🧮 DAX
* To calculate the total_revenue for each month:

```
Total revenue := [Median Price Room]*COUNT(Reservation_Stay_Days[Booking_ID])
```
* To calculate the loss_percentage from cancellations for each month:

```
Loss from Cancellations := 
DIVIDE(
    CALCULATE([Total Revenue], Reservation_Stay_Days[booking_status] = "Canceled"), 
    CALCULATE([Total Revenue], Reservation_Stay_Days[booking_status] = "Not_Canceled"),
    0
)
```

### 💡 Insights

* **June** achieves the highest revenue, with strong bookings (almost as many as October), but its cancellation rate is much lower (71%) compared to October's 91%. This indicates that while October has a higher volume of bookings, it also experiences significantly more cancellations, affecting overall revenue. It benefits from a more stable cancellation rate, which allows for more consistent revenue generation.

* **October**, with the highest number of bookings, likely benefits from a higher volume-driven strategy, but the 91% cancellation rate suggests that more cancellations are reducing its potential revenue. The high volume in October could be a risk if not managed with strategies to reduce cancellations.

* **September** sees the highest median room price (€119) but also a high cancellation rate (81%). This suggests that higher room prices attract premium customers, but cancellations still affect revenue.


![Texto alternativo](hotel_analysis_images/2.png)

### 🤔 So What

* October has the highest bookings but also the highest cancellation rate, impacting revenue. June, with fewer cancellations, generates more stable revenue despite lower bookings. Focusing on reducing cancellations, especially in high-demand months like October, could optimize revenue.

### 3️⃣ How does reservation lead time affect booking status (cancelled vs. not cancelled)?

### 📈Pivot Table
* 📊 I moved the booking_status (Canceled and Not Canceled) and month_name to the rows area, total_bookings_count and median_lead_time into the values area.

### 🧮 DAX
* To calculate the median_lead_time for each month:

```
Median Lead Time := MEDIAN(Reservation_Stay_Days[lead_time])
```
* To calculate the cancellation_probability:

```
  Cancellation Probability := 
    DIVIDE(
        SUM(Reservation_Stay_Days[Canceled]), 
        SUM(Reservation_Stay_Days[Canceled]) + SUM(Reservation_Stay_Days[Not_Canceled])
    )
```

* Reservation lead time is positively correlated with cancellations. As the lead time increases, the probability of cancellation rises.

* September and October show the highest lead times and cancellations. These months have longer booking periods, but they also show higher cancellations.

* February, January and March have low lead times and cancellations, indicating that shorter booking windows are associated with fewer cancellations.

* The not cancelled bookings tend to cluster around lower lead times, showing that guests with short-term bookings are more likely to stick to their reservations.

<img src="hotel_analysis_images/3.png" width="600" height="300">
<img src="hotel_analysis_images/4.png" width="600" height="300">


### 🤔 So What
* Longer lead times result in a higher likelihood of cancellations, which suggests that strategies such as reducing lead times or offering incentives to prevent cancellations could be considered, especially for months like September and October.

* Shorter lead times are associated with more stable bookings, which could help forecast and plan more effectively for high-demand months with fewer cancellations.

### 4️⃣  How does reservation room price affect booking status (cancelled vs. not cancelled)?
