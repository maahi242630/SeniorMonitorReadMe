# **A Non-Intrusive Approach to Monitoring Homebound Seniors Living Alone**


My project focuses on the problem of seniors living alone not being unable to get up because they fell or because of sudden acute immobility due to a medical condition. In such situations, the senior may be unable to reach a phone to call a loved one for help, leaving them stranded and at risk of serious complications. 

The purpose of this project is to create a  **non-intrusive passive monitoring device** to monitor a senior that lives alone. The device will **track the motion of the senior and detect irregular activity patterns** that may indicate immobility in real time to notify loved ones.

A major criteria for my proposed solution is that it must be **non-intrusive**. It must operate without requiring any work from the senior. Additionally, it must not invade the privacy of the senior.

The prototype evolved with time and had multiple iterations.

# **Prototype Details**
The linked documents provides information about the problem, design constraints, design and Methodology, execution.<br/>
[About the Project](https://docs.google.com/document/d/1Zia1dOKYD_Fthd--eugoCcRRx_E7b84Enq3M3UmAU7g/edit?tab=t.0)


# **Prototype Evolution** 
The prototype evolved over multipe iterations

## **Iteration 1** 
    Features
        * Monitored the slots specified in the configuration file. 
        * At the end of the monitoring duration, it checked for motion detection. 
        * If no motion was detected, it made a call to the loved one using Twilio web communication APIs.
## **Iteration 1** <br/> 
[Source Repository](https://github.com/maahi242630/seniormonitor-Version-1) - https://github.com/maahi242630/seniormonitor-Version-1

## **Iteration 2** 
    Features
        * Enhanced with Adaptive Monitoring slots derived using Open AI web API
        * Recorded time stamps whenever motion was detected
        * Fewer than 3 days of recorded timestamps resulted in device operation in Training Mode. During Training Mode, simply record the timestamps.
        * If motion was not detected in the expected time slots or motion was detected across all time slots, the application made an alarm call to the loved one.

## **Iteration 2**
[Source Repository](https://github.com/maahi242630/seniormonitor-Version-2) - https://github.com/maahi242630/seniormonitor-Version-2

## **Iteration 3**
    Features
        * Enhanced with Adaptive Statistical Analysis Monitoring Algorithm using Mean, Standard Deviation and Z-Score
        * Recorded time stamps whenever motion was detected in dated files
        * Divided a day in half hour slots
        * Used the previous 5 days of timestamps. Aggregated these timestamps across half hour slots. Found mean and standard deviation across corresponding slots across 5 days. Used this to come up with reference data.
        * Tracked motion detected count for the monitored day slots.
        * Slot level Anomaly check
            For the slot that just ended:
            x = today’s count for that slot.
            z = (x - mean[i]) / max(std[i], 0.5).
            If |z| >= k (e.g., k=3.0), the application raises the alarm
            This catches both unusually low activity (possible inactivity risk) and unusually high activity (possible restlessness, wandering).
## **Iteration 3**
[Source Repo](https://github.com/maahi242630/seniormonitor-Version-3) - https://github.com/maahi242630/seniormonitor-Version-3

## **Observations**
    The prototype provided promising results when the monitored subject had a repetitive daily schedule near the prototype.
    The sensor was prone to false motion detection. Using standard deviation and Z-score for calculation mitigated the impact of false motion detection to an extent.
    The prototype resulted in some false alarm calls. This is acceptable in scenarios where calls are dialled to family members. 
    Significant routine changes on a given day resulted in false alarms. This continued for the next few days as the impact got carried over.
    Z score of 3 provided optimized results and minimized false alarms.

## **Test Scenarios**
    The prototype was test run in 5 different scenarios
    These are captured in the following sheet.
