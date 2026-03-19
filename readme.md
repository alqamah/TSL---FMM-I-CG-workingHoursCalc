this app calculates the total-working-hours of every employee from the clm data uploaded.

Other features:

calculates the aggregate of skill-wise and employee-wise hours.

handles most of the edge cases unlike CLM.

has a feature to add lunch hours to the total working hours.

assigns the shift based on the punch-in and punch-out times, and from the list of allowed shifts for each employee.

has a feature to export the data to an excel file.


### Duty In (Check-In) Time Logic

| Scenario | Condition | Duty In Assigned | Example |
| :--- | :--- | :--- | :--- |
| **Early OT** | Checked in > 59 mins early AND `allowedOT.in` is true | Rounded UP to the next 30 minutes | Shift 08:30. Arrived 06:50 ➔ Duty In 07:00 |
| **Normal / Grace** | Checked in anywhere up to 15 mins late OR slightly early | Exact Shift In time | Shift 08:30. Arrived 08:42 ➔ Duty In 08:30 |
| **Late** | Checked in > 15 mins late | Rounded UP to the next 30 minutes (Penalty) | Shift 08:30. Arrived 08:47 ➔ Duty In 09:00 |

### Duty Out (Check-Out) Time Logic

| Scenario | Condition | Duty Out Assigned | Example |
| :--- | :--- | :--- | :--- |
| **Early Leaver** | Pulled out before shift end time | Rounded DOWN to previous 30 minutes (Penalty) | Shift ends 17:30. Left 17:15 ➔ Duty Out 17:00 |
| **OT Out** | Stayed past shift end AND `allowedOT.out` is true | Rounded DOWN to previous 30 minutes | Shift ends 17:30. Left 18:25 ➔ Duty Out 18:00 |
| **Normal Leave** | Left at or past shift end but no OT allowed | Exact Shift Out time | Shift ends 17:30. Left 18:15 ➔ Duty Out 17:30 |