# DA_Analysis_on_charges
Analysis on the charges levied by their Delivery partners to X company per Order are correct or not

## Problem statement

Client has a large ecommerce company in India (let’s call it X). X gets a thousand orders via their website on a daily basis and they have to deliver them as fast as they can. For delivering the goods ordered by the customers, X has tied up with multiple courier companies in India as delivery partners who charge them some amount per delivery. <br><br>
The charges are dependent upon two factors: <br>
  -  Weight of the product and the Price of the product. 
  -  Distance between the warehouse (pickup location) and customer’s delivery address 
  (destination location) <br><br>
On an average, the delivery charges are Rs. 100 per shipment. So if X ships 1,00,000 orders per month, they have to pay approximately Rs. 1 crore to the courier companies on a monthly basis as charges. 
As the amount that X has to pay to the courier companies is very high, they want to verify if the charges levied by their Delivery partners per Order are correct.

## Summary of the Approach
Import libraries: 
Importing several essential Python packages to enable various functionalities within the project. 
	

**Workflow:**
1. Reading Data:<br>
  Load the required data files into Data-frames.
2. Converting Zone Values:<br>
  Ensure uniformity by converting zone values to lowercase.
3. Calculating Total Price:<br>
  Calculate the total price for each order item based on the item price and quantity.
4. Merging Data-frames and Grouping content:<br>
  Merging Weight for item from SKU_report to order_report and calculating total weight of the order by group the data-frame by order_id and agg() required column with appropriate aggregate function.
  Initially we had 400 data-point the order report which is a item wise data-point, After doing necessary amendment it’s grouped-by order wise data-point and we have 124(match with all other report)
5.  Merging Other dataframes:<br>
Upon grouping by order_id, now we are merging list of  data-point from other data-frames.<br>
  a)Customer Pin_code From Invoice report<br>
  b)Zone from Pin-code report<br>
  c)Rate slab from courier company rate card<br>
  d)AWB code, Charged weight, zone mentioned by courier company, type of shipment and bill charged by courier company from invoice report<br>
  e)Reassigning and arranging column which are required<br>
6.  Weight Conversion and weight applicable:<br>
Calculated weight per orders are in grams and the slabs are mentioned in kgs so to make all uniform, we are converting our product weights to kgs and creating new columns that covers applicable weight as slabs for charges consideration.
7.  Courier Charges Criteria: <br>
  Points to consider for calculating courier charges<br>
  ⭐Zone: This plays vital role when we calculating the courier charges since it’s distance between warehouse and delivery location.<br>
  ⭐Shipment Type: FWD only or FWD with RTO<br>
  ⭐Weight Slab: First fixed weight and additional with for both FWD and RTO <br>
  ⭐Payment mode: Prepaid or COD(flat15 or 5% based on value of the order)<br>
The below function will take all these point to the consideration and it will return the total charges for particular order <br>
8.  Expected Charge as per X:<br>
  Creating a new column passing data-points to the above function and placing expected charges in it.<br>
9.  Difference in Charges:<br>
  By step we will get rough idea on the difference of charges between X company and courier company whether they charged correctly or over/under charged for the couriers.<br>
10.  Column renaming and downloading:<br>
  We got desired output for the first task, before make a copy we need to rename the columns as per expected result file and below are the codes to rename and make copy of it<br>
11.  Charges Categorization:<br>
  The data frame has been filtered into three category:<br>
  ⭐Correctly charged<br>
  ⭐Overcharged<br>
  ⭐Undercharged<br>
  And made a separate data-frame for it to understand it and access easily, also made a copy in excel for second task
![image](https://github.com/selvamani1992/DA_Analysis_on_charges/assets/127743694/b6b827a0-11b3-4fee-859f-008ae5667e51)

## Insights on the occurrence:
Comparison ratio of count and amount between each category:<br>
![image](https://github.com/selvamani1992/DA_Analysis_on_charges/assets/127743694/9d3f53d0-316c-4095-b49c-14b92b89455c)

**Correctly charged** category is very less compare to other two categories<br>
    9% on total orders <br>
    4% on total value <br>
  In terms of revenue, company X is in a profitable zone. The undercharged amounts are significantly higher compared to the overcharged amounts. However, when it comes to order count, 55% of the orders are charged above the committed cost. <br>

**Incorrect zone on Overcharge:** <br>
  One of the main reasons for overcharging is the incorrect zone assignment.<br>
  Out of the 68 overall overcharged orders, 41 of them were charged with the wrong zone.<br>
  It is important to note that all **41 orders actually belong to Zone B,** but the courier company mistakenly mentioned Zone D.<br>
  For Zone B, the minimum weight slab is **500g, and the rate is Rs. 33** per kg for forward shipments. In contrast, for   Zone D, the minimum weight slab is **1.25kg, and the rate is Rs. 45.4** for forward shipments.<br>
  There are a few incorrect zones in the undercharged category, but looks like those have been compensated with other benefits.<br>
**COD charges on Undercharges:** <br>
  Most of the orders in the undercharged categories belong to COD payment, and it seems that the percentage calculation of COD charges is different for high-value products.<br>
  The top 5 orders in the undercharged category are characterized by high values, less weight, and cash on delivery (COD). However, the courier charges for these orders are almost the same as those for normal orders.<br>

## Suggestion to X company for consideration:
-  For the utmost accuracy in zone selection, it would be highly beneficial to communicate with the courier company and emphasize the importance of performing a double check. This step will ensure that any errors or inaccuracies are minimized, leading to smoother deliveries and happier customers. Additionally, consider suggesting an update to their system that automatically fills in the correct zone information. This would not only save time but also provide a reliable solution for consistent and error-free order processing.
-  In the event that the courier company makes any changes to the zone list, kindly obtain the revised version and ensure that our organization's system is promptly updated. 
-  Please make sure to collect the updated list of COD charges and keep it handy for future reference. This will help you accurately calculate any additional costs associated with cash on delivery transactions..
-  Efficiently managing courier charges is crucial for any business. By closely monitoring these expenses and consistently communicating with the vendor, you can work towards minimizing them to a great extent. Whether the charges are under or over what is expected, it's important to address and resolve them promptly in order to achieve cost savings.
