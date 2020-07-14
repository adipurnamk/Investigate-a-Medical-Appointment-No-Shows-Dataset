## Introduction

>This dataset collects information from 100k medical appointments in Brazil and is focused on the question of whether or not patients show up for their appointment. A number of characteristics about the patient are included in each row.

**Data Dictionary** based on original dataset in [Kaggle](https://www.kaggle.com/joniarroba/noshowappointments).
1.  PatientId | Identification of a patient  
2.  AppointmentID | Identification of each appointment
3.  Gender | Male or Female, Female is the greater proportion, woman takes way more care of they health in comparison to man.
4. ScheduledDay | The day of the actuall appointment, when they have to visit the doctor.
4. AppointmentDay | The day someone called or registered the appointment, this is before appointment of course.
5. Age | How old is the patient.
7. Neighbourhood | Where the appointment takes place.
8. Scholarship | True of False . Observation, this is a broad topic, consider reading this [article](https://en.wikipedia.org/wiki/Bolsa_Fam%C3%ADlia).
9.  Hipertension | True or False
10. Diabetes | True or False
11. Alcoholism | True or False
12. Handcap | True or False
13. SMS_received | 1 or more messages sent to the patient.
14. No-show | True or False.

**Question**  
What factors are
important for us to
know in order to
predict if a patient will
not show up for their
scheduled
appointment?

---

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

>So for the health center, it's better to set the appointment day in working day with no more than one week waiting days


---

## Reference
* [Numpy Documentation](https://numpy.org/doc/)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Matplotlib Documentation](https://matplotlib.org/3.2.1/contents.html)
* [Seaborn Documentation](https://seaborn.pydata.org/index.html)
* [Applying heatmaps for categorical data analysis](https://www.kaggle.com/tsilveira/applying-heatmaps-for-categorical-data-analysis#[5])
* [Data Analyst Nanodegree project - first attempt](https://www.kaggle.com/kuroski/data-analyst-nanodegree-project-first-attempt)
* [pandas dataframe group and sort by weekday](https://stackoverflow.com/questions/47741400/pandas-dataframe-group-and-sort-by-weekday)