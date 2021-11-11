# data

## f1merged

- `raceId`: Foreign key link to races table
- `year`: Foreign key link to seasons table     
- `round`: Round number
- `racename`: Race name
- `date`: Race date e.g. "1950-05-13"
- `driverId`: Foreign key link to drivers table    
- `driverRef`: Unique driver identifier
- `surname`: Driver surname
- `constructorId`: Foreign key link to constructors table
- `constructorRef`: Unique constructor identifier
- `constructorname`: Constructor name
- `constructornat`: Constructor Nationality
- `resultId`: Foreign key link to results table
- `number`: Driver number 
- `grid`: Starting grid position
- `position`: Official classification, if applicable
- `positionText`: Driver position string e.g. "1" or "R"
- `positionOrder`: Driver position for ordering purposes
- `points`: Driver points for race
- `laps`: Number of completed laps
- `time`: Finishing time or gap   
- `milliseconds`: Finishing time in milliseconds
- `fastestLap`: Lap number of fastest lap
- `rank`: Fastest lap rank, compared to other drivers
- `fastestLapTime`: Fastest lap time e.g. "1:27.453"
- `fastestLapSpeed`: Fastest lap speed (km/h) e.g. "213.874"
- `statusId`: Foreign key link to status table

## Labels used in the positionText fields:                          
- `D` - disqualified                                             
- `E` - excluded                                                
- `F` - failed to qualify                                       
- `N` - not classified                                           
- `R` - retired                                                 
- `W` - withdrew       

## circuits

- `circuitId`: Primary Key 
- `circuitRef`: Unique circuit identifier
- `name`: Circuit name
- `location`: Location name
- `country`: Country name  
- `lat`: Latitude 
- `lng`: Longitude
- `alt`: Altitude (metres)
- `url`: Circuit Wikipedia page


## constructor_results

- `constructorResultsId`: Primary Key 
- `raceId`: Foreign key link to races table
- `constructorId`: Foreign key link to constructors table
- `points`: Constructor points for race
- `status`: "D" for disqualified (or null)  

## constructor_standings

- `constructorStandingsId`: Primary Key 
- `raceId`: Foreign key link to races table
- `constructorId`: Foreign key link to constructors table
- `points`: Constructor points for season
- `position`: Constructor standings position (integer)
- `positionText`: Constructor standings position (string)
- `wins`: Season win count

## constructors

- `constructorId`: Primary key     
- `constructorRef`: Unique constructor identifier
- `name`: Constructor name
- `nationality`: Constructor Nationality
- `url`: Constructor Wikipedia page

## driver_standings

- `driverStandingsId`: Primary key     
- `raceId`: Foreign key link to races table
- `driverId`: Foreign key link to drivers table
- `points`: Driver points for season
- `position`:  Driver standings position (integer)
- `positionText`: Driver standings position (string) 
- `wins`: Season win count

## drivers

- `driverId`: Primary key     
- `driverRef`: Unique driver identifier
- `number`: Permanent driver number
- `code`: Driver code e.g. "ALO"
- `forename`: Driver forename
- `surname`: Driver surname
- `dob`: Driver date of birth
- `nationality`: Driver nationality 
- `url`: Driver Wikipedia page

## lap_times 

- `raceId`: Foreign key link to races table     
- `driverId `: Foreign key link to drivers table
- `lap`: Lap number
- `position`: Driver race position 
- `time`: Lap time e.g. "1:43.762"  
- `milliseconds`: Lap time in milliseconds  

## pit_stops

- `raceId`: Foreign key link to races table     
- `driverId `: Foreign key link to drivers table
- `stop`: Stop number 
- `lap`: Lap number
- `time`: Time of stop e.g. "13:52:25"     
- `duration`: Duration of stop e.g. "21.783" 
- `milliseconds`: Duration of stop in milliseconds 

## qualifying

- `qualifyId`: Primary Key
- `raceId`: Foreign key link to races table     
- `driverId `: Foreign key link to drivers table
- `constructorId`: Foreign key link to constructors table
- `number`: Driver number
- `position`: Qualifying position
- `q1`: Q1 lap time e.g. "1:21.374"   
- `q2`: Q2 lap time
- `q3`: Q3 lap time 

## races 
- `raceId`: Primary Key
- `year`: Foreign key link to seasons table    
- `round`: Round number
- `circuitId`: Foreign key link to circuits table
- `name`: Race name
- `date`: Race date e.g. "1950-05-13"
- `time`: Race start time e.g."13:00:00"   
- `url`: Race Wikipedia page

## results

- `resultId`: Primary key
- `raceId`: Foreign key link to races table
- `driverId`: Foreign key link to drivers table    
- `constructorId`: Foreign key link to constructors table
- `number`: Driver number 
- `grid`: Starting grid position
- `position`: Official classification, if applicable
- `positionText`: Driver position string e.g. "1" or "R"
- `positionOrder`: Driver position for ordering purposes
- `points`: Driver points for race
- `laps`: Number of completed laps
- `time`: Finishing time or gap   
- `milliseconds`: Finishing time in milliseconds
- `fastestLap`: Lap number of fastest lap
- `rank`: Fastest lap rank, compared to other drivers
- `fastestLapTime`: Fastest lap time e.g. "1:27.453"
- `fastestLapSpeed`: Fastest lap speed (km/h) e.g. "213.874"
- `statusId`: Foreign key link to status table

## seasons 

- `year`: Primary key e.g. 1950
- `url`: Season Wikipedia page

## status 

- `statusId`: Primary key
- `status`: Finishing status e.g. "Retired"

   


