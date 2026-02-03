# Project-1-Actual
import pandas as pd

air_data = pd.read_csv('AirQuality_Daily_StudentVersion.csv')

air_data = pd.DataFrame(air_data)
#VOC
correct_air_groups = air_data.groupby('sensor.name')
print(correct_air_groups)

correct_air_summary = correct_air_groups.agg(
                                             mean = ('voc','mean'),
                                             median = ('voc','median'))

top5_mean_voc = correct_air_summary.nlargest(5, "mean")
print(top5_mean_voc)

top5_median_voc = correct_air_summary.nlargest(5, "median")
print(top5_median_voc)

#PM2.5
pm25_groups = air_data.groupby('sensor.name')
print(pm25_groups)

pm25_summary = pm25_groups.agg(
                                             mean = ('pm2.5_atm','mean'),
                                             median = ('pm2.5_atm','median'))

top5_mean_pm25 = pm25_summary.nlargest(5, "mean")
print(top5_mean_pm25)

top5_median_pm25 = pm25_summary.nlargest(5, "median")
print(top5_median_pm25)

#PM10.0
pm10_groups = air_data.groupby('sensor.name')
print(pm10_groups)

pm10_summary = pm10_groups.agg(
                                             mean = ('pm10.0_atm','mean'),
                                             median = ('pm10.0_atm','median'))

top5_mean_pm10 = pm10_summary.nlargest(5, "mean")
print(top5_mean_pm10)

top5_median_pm10 = pm10_summary.nlargest(5, "median")
print(top5_median_pm10)




#voc max
correct_air_groups = air_data.groupby(['sensor.name','date'])
correct_air_summary = correct_air_groups.agg(max = ('voc','max')) 
voc_max = correct_air_summary.nlargest(1,'max')
print(voc_max)

#pm2.5 max
pm25_groups = air_data.groupby(['sensor.name','date'])
pm25_summary = pm25_groups.agg(max = ('pm2.5_atm','max')) 
pm25_max = pm25_summary.nlargest(1,'max')
print(pm25_max)

#pm10.0 max
pm10_groups = air_data.groupby(['sensor.name','date'])
pm10_summary = pm10_groups.agg(max = ('pm10.0_atm','max')) 
pm10_max = pm10_summary.nlargest(1,'max')
print(pm10_max)



#TEMPERATURE
import pandas as pd
air_data = pd.read_csv('AirQuality_Daily_StudentVersion.csv')
air_data = pd.DataFrame(air_data)

def assign_temperature(temperature):
    if temperature < 32:
        return 'Below Freezing'
    elif 32 <= temperature <= 50:
        return 'cool'
    elif 52 <= temperature <= 70:
        return 'Warm'
    else:
        return 'Hot'

air_data['temperature_level'] = air_data['temperature'].apply(assign_temperature)
#air_data.head(10)
#VOC
hot_air = air_data[air_data['temperature_level'] == 'Hot'].groupby(['voc','temperature','temperature_level'])
hot_air_mean = hot_air.agg(mean = ('voc','mean'))
hot_pollution = (hot_air_mean.sort_values(by = 'mean',ascending = False).head(10))

#PM2.5

hot_air2 = air_data[air_data['temperature_level'] == 'Hot'].groupby(['pm2.5_atm','temperature','temperature_level'])
hot_air_mean2 = hot_air2.agg(mean = ('pm2.5_atm','mean'))
hot_pollution2 = (hot_air_mean2.sort_values(by = 'mean',ascending = False).head(10))

#PM10.0

hot_air3 = air_data[air_data['temperature_level'] == 'Hot'].groupby(['pm10.0_atm','temperature','temperature_level'])
hot_air_mean3 = hot_air3.agg(mean = ('pm10.0_atm','mean'))
hot_pollution3 = (hot_air_mean3.sort_values(by = 'mean',ascending = False).head(10))
print([hot_pollution,hot_pollution2,hot_pollution3])



#HUMIDITY
import pandas as pd
air_data = pd.read_csv('AirQuality_Daily_StudentVersion.csv')
air_data = pd.DataFrame(air_data)

def assign_humidity(humidity):
    if humidity < 50:
        return 'Low humidity'
    elif 51 <= humidity <= 80:
        return 'High humidity'
    else:
        return 'Very High Humidity'

air_data['humidity_level'] = air_data['humidity'].apply(assign_humidity)

#VOC - humidity
hot_air11 = air_data[air_data['humidity_level'] == 'Very High Humidity'].groupby(['voc','humidity','humidity_level'])
hot_air_mean11 = hot_air11.agg(mean = ('voc','mean'))
hot_pollution11 = (hot_air_mean11.sort_values(by = 'mean',ascending = False).head(10))

#PM2.5 - humidity

hot_air22 = air_data[air_data['humidity_level'] == 'Very High Humidity'].groupby(['pm2.5_atm','humidity','humidity_level'])
hot_air_mean22 = hot_air22.agg(mean = ('pm2.5_atm','mean'))
hot_pollution22 = (hot_air_mean22.sort_values(by = 'mean',ascending = False).head(10))

#PM10.0 - humidity

hot_air33 = air_data[air_data['humidity_level'] == 'Very High Humidity'].groupby(['pm10.0_atm','humidity','humidity_level'])
hot_air_mean33 = hot_air33.agg(mean = ('pm10.0_atm','mean'))
hot_pollution33 = (hot_air_mean33.sort_values(by = 'mean',ascending = False).head(10))
print([hot_pollution11,hot_pollution22,hot_pollution33])




import pandas as pd
air_data = pd.read_csv('AirQuality_Daily_StudentVersion.csv')
air_data = pd.DataFrame(air_data)

unhealthy1 = air_data[air_data['pm10.0_atm'] > 155].groupby(['sensor.name','date'])
unhealthy_median = unhealthy1.agg(median = ('pm10.0_atm','median'))
unhealthy_voc = unhealthy_median.sort_values(by = 'median', ascending = False).head(8)

unhealthy_voc
