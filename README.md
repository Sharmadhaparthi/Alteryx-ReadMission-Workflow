# Alteryx-ReadMission-Workflow

This workflow demonstrates how you can calculate repeating events within a relatively defined timeframe, such as readmissions to a hospital within 30 days of a trigger event (the initial discharge). 

•	Data is loaded using the **input data tool**.

•	Fields of interest like Record_id, Patient_id, Admission_date and Discharge_date are selected using **select tool**.

•	Custom Filtration on condition admission date and discharge date cannot be empty is applied using **filter tool**.

•	Discharge_date is sorted in ascending order using **sort tool**.

•	DaysSinceLastDischarge field value is calculated usig **multi row formula** using the expression DateTimeDiff([AdmitDate],[Row-1:DischargeDate],'days')

•	Anchor Date Field is created and using the **formula tool** flag value is set to 1 if the date frame is outside DaysSinceLastDischarge field value.

•	The anchor date for records that are recurrences are updated with the anchor date from the first occurrence. The **multi-row tool** here makes it possible that this updates for ALL occurrences within the time frame. For all records that are stand-alones  they keep their own start date.

•	DaysSinceLastDischarge, IsAnchor, AnchorDischargeDate are included in the visibility using select tool.

•	Again, using **formula tool** time between the anchor event and the current event is calculated via **DateTimeDiff function**.

•	Then, using **multi row formula** flags from records that belong to an episode that's already been flagged.

•	Using **formula tool**, read mission flag is calculated based on condition If [DaysSinceAnchor]>0 AND [DaysSinceAnchor]<30 then 1 else 0 endif

•	The summation of the readmission flag, summation of the readmission flag grouped by count and overall view of all fields along with individula readmission flag values can be viewed using **browse tool**.

