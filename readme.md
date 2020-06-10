>Before proceed to the next step, firstly we need to import some useful modules that we are using in this project.
> 1. Numpy for scientific computing with Python.
> 2. Pandas as data manipulation and analytic tool for Python.
> 3. Matplotlib basic tool for making data visualization
> 4. Seaborn for beautifying the visualization

>From the CSV file *noshowappointments-kagglev2-may-2016.csv*, we got the data frame which has 110527 rows and 14 columns (as stated in dataset dictionary)  

>Then, we want to see the information from this data frame, from this we can know if there is missing data in it.

> * The data frame contains no missing value.
> * Columns name is pretty consistent with *title* style. For easier to query, we will transform it into lower style
> * The PatientId should be in object data type, to prevent it from the calculation
> * The ScheduledDay and AppointmentDay should be in DateTime data type, maybe we should add the period columns too.

>First, we need to determine what columns we should explore. Since 'PatientId', 'AppointmentID', 'ScheduledDay' and 'AppointmentDay' mostly unique for each rows, we should skip these columns.

> In the next step, we have to change the handicap and no-show column values to binary values.

### Data Cleaning

#### Renaming the Columns

>The columns name use combination of capital letters, it makes the data manipulation more difficult. We should change it into a lower style.
>Then for improving readability, we add underscore in the non-single string column.

#### Drop appointment_id Column

>I think we do not need the appointment_id column because it will be different for each row. Also, we cant be certain enough to get some insight from it, analysis will be better if we use the DateTime-based column.

#### Data Type Casting

The patient_id column is not intended to be calculated, so, we cast it into object data type.

>For scheduled_day and appointment_day, as the data inside it has been formatted in DateTime, we cast it into DateTime data type.

> For assure, we check using .info() method

#### Categorical Data
>We' will convert the handicap and no-show column into binary categorical data.

As for the handicap column, we will convert values more than one into 1.

#### Adding some  New Columns

>We need to add two new columns; appointment_day and time_span between scheduled_day and appointment_day.

We can get time_span value with decreasing appointment_day by scheduled_day.

Then, to get an appointment_weekday we can convert appointment_day DateTime into day name.

#### Examine Weird Data

>Next, we need to examine from the summary statistic, to see if there is some weird data in it.

>That's it. There is some weird data in the age column. The age is less than 0, is it possible?  
We will examine it further.

>The patient with id number 465943158731293 has age -1. Since it just one row we will drop that row.

>Notice that the row is decreased by one after dropping the weird data.

<a id='eda'></a>
## Exploratory Data Analysis

>Now we have trimmed and cleaned our data, we're ready to take the next step.
In the Exploratory Data Analysis section, we will compute the statistic and doing some basic data visualization. To reach our goal, we need to explore each variable.

>First, we need to look at our last data frame that has been cleaned before.

### How is the proportion of no_show column value?
> Before exploring further, we need to know the state of the data.

>From the pie chart above, we can see that more than 20% percent of patients are not showing.   

### How is data distribution?

>Then, we need to know how data is distributed. We are using the .hist() method on our data frame.

> From the bar plots and summary statistics above, mostly the patients are:
* Under 60
* Not alcoholism
* Not in diabetes
* Female in gender (as stated in the dictionary)
* Have no handcap
* Not in hipertension
* Not in scholarship
* Not received any SMS
* Time span is equal and under two weeks

Too, from these bar plots, we know that some binary-value columns i.e, gender, scholarship, hipertension, diabetes, alcoholism, and handcap.

### Binary-Value Columns and no_snow Column
>Before exploring the binary-value columns, we need to make a crosstab function.
This function will compute the frequency for each variable.

>In this step we need to contain our binary-value columns into some container, such as a list.
Then we iterate through that container while applying crosstab function on it.


> The difference rate is so small, for gender, scholarship, hipertension, diabetes, alcoholism, and handcap is no more than 5%. So we cannot use these variables for no_show deciding factor.

> Except for the sms_received column which the difference rate is more than 10%. Maybe we can use this as a deciding factor. Although it's kinda weird, the patient who received SMS showing that more no_show rate than non received SMS.

### Age

> Same as binary-value columns, we need to apply crosstab function on the age column. Then plot the rate value into a scatter plot to see the variable correlation.

>The trend shows us that younger patients tend to not attend the appointment day. This trend is decreased along with the increasing age.

> At the most right of the plot, there is one point that has the highest no-show rate (age=115). This point is an outlier as shown in the following boxplot, so we can ignore it.

### Time Span
> In Data Cleaning section we has added the time span column. Then we apply the crosstab function to this column.
<li><a href="#add">Time Span Calculation</a></li>

> This plot produces a trend that is difficult to see, whether it goes up or down during time_span. By using .corr() method we know that the trend is increasing along the time_span, but the value is so small.

> For the same day waiting time the no show rate is so small, it' just 6.63%. Then this rate is jumped high when the waiting time is not on the same day. Starting in the short term, the rate is 23.6%. This value is increasing along as waiting time increased. This trend happened until quarter term, which is the highest no show rate for the time span variable, 33.11%. At the semester term, the no showing rate is decreased, it's just 27.3%.

>It's seems that almost all neighborhood has the same rate of no showing patients, the mean is  20.54%.
Because the dataset is lack of information about the dataset source location or certain hospital, we cannot sure neighbourhood variable can be used for predicting.


> From the barplot above, the highest no showing rate is happening on Saturday which is 23.08%. Actually, the trend is increased from Friday.
> There is no appointment that happened on Sunday, we can know that health services on Sundays are closed.
> Starting Sunday to Thursday the no showing trend is decreasing along the weekdays
> People tend to not coming to the health center in the weekend, or a day before the weekend
> From this insight, we can take appointment_weekdays as variable to determine no showing patient rate.

<a id='conclusions'></a>
## Conclusions

> In the <a href="#intro">Introduction</a> section we have state a question "What factors are important for us to know in order to predict if a patient will not show up for their scheduled appointment?". From the exploratory we did before, we can certain these variables may be a good predictor:
* SMS Received
* Age
* Time Span
* Appointment Weekday

**Limitation**
> The limitation that we have in this dataset is, this dataset does not provide a certain location of the health center. Maybe the neighborhood can be a good predictor variable.

**Recommendation**
> From this dataset, people tend to come for an appointment if: 
* the waiting day is short 
* not at the weekend
So for the health center, it's better to set the appointment day in working day with no more than one week waiting days