# Synchronicity Data Science FCC

This jupyter notebook was created as part of the Synchronicity project to assist the Impact Assessment team with their analysis. From all soucring data, only the car parking sensors in Santander City Centre with data collected between May and August this year (2018-05-09 to 2018-08-1) were used. The dataset was sourced by placing requests on Santander’s smart parking API (http://datos.santander.es/api/rest/datasets/sensores_smart_parking.json) every minute and storing the dataset in a mongodb database. The API’s response consisted of information such as location of the sensor, a timestamp when the status of the sensor was last updated, the status of the sensor (occupied/free) as well as sensor id. 
The resulting dataset was then used to provide insights on the parking habits of drivers for the areas where sensors are installed.

To have an indication of the parking flux at street level, the sensors were grouped by street location, resulting in 8 categories. Next, for the whole data sourcing period, the number of times the parking status was reported occupied versus free were calculated for each time of day. Finally, the ratio between these frequencies was taken as a proxy of parking availability ranging from 0-1 (free/occupied). 

Furthermore, the total duration cars spend parked at spot is an important attribute that is likely to influence any availability recommendations based on historical data. To get an insight on the total duration a parking spot remained occupied, the following metric was devised:
For every sensor check whether the occupancy status had status: occupied. If so, store the sensor’s status update time.
Move to the subsequent record in the dataset and check whether the occupancy  status remains: occupied. If so, move to the next record. If not, calculate the duration between the timestamp of the first occurrence of occupied status and the last occurrence of occupied status. 
Store the total duration for the date/time of the first occurrence of occupied status.
Repeat the process.           
This will produce an indication of high likely it for a parking spot to remain occupied in the future, given the current timestamp. The following figure illustrates the variation of duration of occupancy per day of week and time of day.  

