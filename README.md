# citibike-tableau
## Description
Using the Citi Bike System Data found on <https://www.citibikenyc.com/system-datareate>, create and analyze visualizations of unexpected phenomena for a chosen time period with Tableau. You can find the link to my workbook at <https://public.tableau.com/profile/nick.mangarella#!/vizhome/JerseyCityCitiBikeAnalysis/Story1>.

## data-merge
For this project I decided to analyze the Jersey City datasets for the months of August 2018 and 2019, due to file size and limitations within Tableau Public. Upon downloading the datasets for each month I used Python: OS, Glob, and Pandas to merge them together and change the 'gender' column values from binary to strings for easier handling within Tableau. I then exported this merged dataset to a CSV to be uploaded to Excel.
```
# Use the path to store the csvs into a list
all_files = glob.glob(os.path.join(path, "JC-20*.csv"))
all_files


# Read in the data files and store as one DataFrame
df = (pd.read_csv(i, sep=',') for i in all_files)
df = pd.concat(df)

# Replace binary values for strings
gender = {0: "unknown", 1: "male", 2: "female"}

df["gender"] = [gender[i] for i in df["gender"]]


# Export combined data to a csv
df.to_csv("data/JC-201808-201908-tripdata.csv", index=False)
```

## Jersey City Citi Bike Analysis
The first unexpected phenomena I found when looking at the the Avg. Trip Duration by Age chart. In Auguest of 2018 the highest average trip duration was 183.6 minutes for 20 year olds, however in 2019 20 year olds averaged only 24 minutes per trip. Also in 2019 there was higher spike in average trip duration for people 80 years and older. This suggests that more young users than the previous year provided false birthyears and changed to much shorter routes. Using the Jersey City Median Age map I was able to exclude the possibility of a drastic change in age demographics of the area. Some causes to consider is a possible price jump from 2018 to 2019 in rides longer than 40 minutes or the difference in August weather from one year to the other. Another unexpected phenomena I encountered was the amount of male to female Citi Bike users. While there was an increase in overall users across all gender types from August 2018 to 2019, males were still the majority Subscriber/Customer base eventhough Jersey City has a female dominant populus. One reason to consider is the possibility many females are wearing dresses in the summer month of August and are uncomfortable riding a bike even though they are designed to accomodate dresses. Additionaly women with long hair might find riding a bike and being exposed to wind less suitable for them. Looking into the maps of the Most Popular Start Stations and Most Popular End Stations it can be inferred most Citi Bike users are using the service to commute to locations of public transportation from Jersey City to New York City for work purposes. Grove St PATH and Newport PATH are two of the most heavily used stations and are named after the PATH train stations located there. I also found the most active stations are in zip codes that contain some of the highest income earners. This alludes that the cost to subscribe/purchase a pass is for the higher income earner. One interesting observation that sets both maps apart is there are 53 start stations compared to 78 end stations so there are some people willing to take a bike from one state to another and their is a market for longer rides.
