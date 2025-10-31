# Hospital-Emergency-Department-Queue

1. High-Level Problem Statement

  The Emergency Department (ED) at Metropolis General Hospital is struggling with chronic overcrowding and escalating patient length of stay (LoS). The primary operational failure is the consistent inability to meet the national quality benchmark of having 90% of all ED patients discharged or admitted within 4 hours of arrival. This issue is primarily driven by:

* Stochastic Patient Arrivals: Unpredictable surges in patient volume, especially during peak hours (evenings and weekends).
* Variable Service Times: The time required for diagnosis, testing, and treatment varies dramatically based on triage acuity (CTAS score).
* Downstream Bottleneck (Boarding): The lack of available inpatient beds forces admitted patients to remain in the ED (known as "boarding"), tying up critical ED resources (beds, monitors, staff).

The performance modeling objective is to utilize queueing theory and simulation to identify the optimal resource allocation (staffing and treatment beds) that minimizes patient wait times and maximizes the probability of meeting the 4-hour LoS target, while ensuring high-acuity patients (CTAS 1 & 2) are seen immediately, without unnecessary resource over-provisioning.



2. Defined Performance Objectives

  Performance Aspect	=>  Objective (Metric)	=>  Target/Goal
  
  *  Primary Quality	=>  Length of Stay (LoS)	=>  90% of patients must have a total LoS of <4 hours.
  
  *  Safety/Time	=>  Triage-to-Physician-Seen Time	=>  Median time for CTAS 1 & 2 patients must be <15 minutes.
  
  *  Efficiency/Throughput	=>  System Throughput	=>  Maintain service for the 99th percentile of historical peak hourly arrival rates (e.g., 50 patients/hour).
  
  *  Resource Utilization	=>  Physician & Bed Utilization	=>  Target utilization rate for key physician staff and treatment beds to be in the 85%−95% range.



3. Data Set Description: patient_flow_data.csv

  The dataset provided (patient_flow_data.csv) is a synthetic log based on anonymized historical ED records. It contains key timestamps and characteristics necessary to model the multi-stage queueing system.

  Field Name	=>  Description	=>  Measurable Performance Characteristic
  
  *  Patient_ID	=>  Unique identifier.	=>  N/A
  
  *  Arrival_Time	=>  Timestamp of arrival at the ED front door.	=>  Used to calculate inter-arrival times (Arrival Rate, λ).
  
  *  CTAS_Acuity	=>  Triage score (1=Most Urgent to 5=Least Urgent).	=>  Key Priority variable for the queue discipline.
  
  *  Triage_Start_Time	=>  Time a nurse begins the triage assessment.	=>  Triage Wait Time (Queue 1 Delay).
  
  *  Treatment_Start_Time	=>  Time the patient is placed in a bed/room and seen by a physician.	=>  Bed Wait Time (Queue 2 Delay).
  
  *  Discharge_Time	=>  Time the patient leaves the system (discharged or admitted).	=>  Used to calculate Total Length of Stay (LoS).



  Sample Data Set: patient_flow_data.csv
  
  This sample data is a small excerpt for illustration. The actual file in your repository would contain thousands of rows representing daily or monthly operations.
  
  [patient_flow_data.csv](https://github.com/user-attachments/files/23249032/patient_flow_data.csv)
  Patient_ID,Arrival_Time,CTAS_Acuity,Triage_Start_Time,Treatment_Start_Time,Discharge_Time
  P1001,30/10/2025 14:00,3,30/10/2025 14:05,30/10/2025 14:50,30/10/2025 17:30
  P1002,30/10/2025 14:02,5,30/10/2025 14:08,30/10/2025 15:45,30/10/2025 18:05
  P1003,30/10/2025 14:05,2,30/10/2025 14:05,30/10/2025 14:15,30/10/2025 16:10
  P1004,30/10/2025 14:15,4,30/10/2025 14:20,30/10/2025 16:30,30/10/2025 19:45
  P1005,30/10/2025 14:20,3,30/10/2025 14:25,30/10/2025 15:00,30/10/2025 18:00
