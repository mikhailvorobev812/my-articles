
# [L1] Daily Cluster Sanity Check

## Table of contents

- [General information](#general-information)
- [Daily Cluster Sanity Check](#daily-cluster-sanity-check)
  - [1. Performing checks](#1-performing-checks)
    - [Cluster check](#cluster-check)
    - [Test Client Check](#test-client-check)
    - [Leader Board Check](#leader-board-check)
    - [Azure Service Health](#azure-service-health)
  - [2. Processing cluster check results](#2-processing-cluster-check-results)
    - [Daily Cluster Sanity Check](#daily-cluster-sanity-check-1)
    - [Alert investigation](#alert-investigation)

## General information

**Concurrent Users (CCU)** is the number of people actively connected to a cluster at the same time. This metric is important to understand because it tells us about player load and potential performance impact.

|  | Preprod Clusters (AOETest, AOEFlight) | Prod Clusters (AOELive, Arthurlive, MYTHLive) |
|---|---|---|
| **Who connects** | Only Developers and EdgeLink Members. | Thousands of real players around the globe. |
| **Player activity** | No players are connected here. | Live gameplay sessions happen here. |
| **Impact** | ✅ There will **never** be CCU impact in Preprod because these clusters are not exposed to large-scale player activity. | ⚠️ CCU impact is **only relevant in Prod**, since load can affect stability, latency, and matchmaking. |
| **Example** | If AOETest shows a CCU of 5, that simply means a handful of developers are connected. This does not reflect real player traffic. | **Scenarios of CCU Impact in Prod:**<br><br>1. **High CCU (e.g., 50,000+ concurrent players)**<br>   - Matchmaking times may increase.<br>   - Servers may experience higher CPU/memory usage.<br>   - Some regions could see delays or instability.<br><br>2. **Sudden Spike in CCU (e.g., post-update or event launch)**<br>   - Logins may temporarily fail or slow down.<br>   - Backend services (auth, inventory, etc.) can become bottlenecks.<br><br>3. **Low CCU (e.g., during maintenance or downtime)**<br>   - Fewer reports from players.<br>   - Easier to run hotfix validations and monitoring checks. |
| **Screenshot** |(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%201.jpg) |(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%202.jpg)  |

```
> [!NOTE]
The Daily Cluster Sanity Check should be performed >  **daily (including weekends) at 3:00 AM CDT and 3:00  PM CDT / 2:00 AM CST and 2:00 PM CST**  
(for other time zones,follow the link to the  [time converter](https://www.worldtimebuddy.com/?pl=1&lid=306,30,611717,625144,314,312,206,0,212&h=306&hf=0),
or as part of an alert investigation.
```
# Daily Cluster Sanity Check

## 1. Performing Checks

Within the **Daily Cluster Sanity Check**, perform all 4 checks in the following order:

1. [Cluster check](#cluster-check)
2. [Test Client Check](#test-client-check)
3. [Leader Board Check](#leader-board-check)
4. [Azure Service Health](#azure-service-health)

For **alert investigation**, perform only 2 checks in the following order:

1.  [Test Client Check](#test-client-check)
2.  [Cluster check](#cluster-check)

### Cluster check
1. **For Cluster Check**, open the Cluster's Dashboard by clicking the appropriate link from the list below, depending on the type of check/investigation:
> [!IMPORTANT]
> To perform the Daily Cluster Sanity Check, the following clusters should be checked:
> - **aoelive**
> - **arthurlive**
> - **mythlive**
>
> For **alert investigation**, only the **cluster mentioned in the alert** notification should be checked.

**For daily cluster check:**

-   `aoelive` → [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard)
-   `arthurlive` → [Arthurlive Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/arthurlive-tf-rsg/providers/microsoft.portal/dashboards/arthurlive-monitoring-dashboard)
-   `mythlive` → [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)

**For alert investigation**

-   `aoeflight` → [AOE FLIGHT Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoeflight-tf-rsg/providers/Microsoft.Portal/dashboards/aoeflight-monitoring-dashboard)
-   `aoelive` → [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard)
-   `aoetest` → [AOE TEST Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoetest-tf-rsg/providers/Microsoft.Portal/dashboards/aoetest-monitoring-dashboard)
-   `arthurlive` → [Arthurlive Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/arthurlive-tf-rsg/providers/microsoft.portal/dashboards/arthurlive-monitoring-dashboard)
-   `mythlive` → [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)

2. Set the time range to **Past hour** when investigating alerts. (https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2049.png)
---
>**:warning:Lobby - Total CCU on cluster graph is a Critical Indicator.:warning:** If any gaps or drops are identified, it might indicate a CCU impact issue. Immediately create a new incident as described in **[L1] ADO Ticket Creation**. Escalate it as described in **[L1] Major Incident and MIM Process**, and complete investigation steps afterward.

---
3. Select the **Lobby - Total CCU on cluster** graph.
4. Double-click on the graph to zoom in.
5. Check if there are any any gaps or drops and act accordingly:
---
**During daily EU/APAC check:**
-  **If there are fewer than 5 missing points (or none)**, proceed to Step 6.
-   **If there are **6 or more missing points**/a significant drop**, record this information for **Sev1 Incident creation** and proceed to Step 6.
---
**During daily MX check:**
-   **If there are fewer than 5 missing points (or none)**, proceed to Step 6.
-   **If there are **6 or more missing points**/a significant drop**, ask L2/L3 on the [**EPAM Support** channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams to confirm if a ticket is needed, and follow the instructions. Meanwhile, proceed to Step 6.
---
> **Teams message template:**
> 
> ```
> @everyone, hi team!
> During the cluster check, we found a 5-point gap on <name of the cluster>.
> Please advise if any actions are needed from the L1 team.
> ```
**During alert investigation:** make a  screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Then proceed to step 6.

----------
6. Select the **App Gateway - Backends health (below: unhealthy only)** graph.

7. Check the Unhealthy Backend amount:

   **During daily check:**
   - If Unhealthy Backend is lower than **0.75**, proceed to step 8.
   - If Unhealthy Backend is higher than **0.75**, record this information for **Sev2 Incident creation** after all the checks are finished. Then proceed to step 8.
   - If an unhealthy backend that later recovered was identified, add a comment about that in the e-mail report about the check results. Make a screenshot and attach it as proof to the e-mail report as well. Then proceed to step 8.

   **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 8.

8. Select the **App Gateway - Responses by Status** graph.

9. Double-click on the graph to zoom in.

10. Set the time range to **Past hour** for investigating alerts.

11. Check the number of 4xx and 5xx errors detected and act accordingly:

    **During daily check:**
    - If there are fewer than **3,500** 4xx errors **AND** fewer than **250** 5xx errors, proceed to step 12.
    - If there are more than **3,500** 4xx errors per sample (1 minute), record this information for **Sev2 Incident creation** after all the checks are finished. Then proceed to step 12.
    - If there are more than **250** 5xx errors per sample (1 minute), record this information for **Sev2 Incident creation** after all the checks are finished. Then proceed to step 12.

    **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 12.

12. Select the **Lobby server VMs - CPU usage** graph.
13. Check the thresholds on the graph and act accordingly:
- **During daily check:**
    - **if no thresholds exceed 70%**, proceed to step 14.
    - if any threshold exceeds **70%**, record this information for **Sev2 Incident creation** after all the checks are finished. Then proceed to step 14.

    **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 14.

14. Select the **Battle VMs - CPU usage** graph.
15. Check the thresholds on the graph and act accordingly:
 - **During daily check:**
    - **if any threshold exceeds 70%**, record this information for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the checks are finished.
    - **if no thresholds exceed 70%**, proceed to step 16.

- **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 16.

16. Select the **FlexibleDB/MySQL - CPU/Memory/Storage** graph.

17. Check the usage thresholds:
- **During daily check:**
    - **if any threshold exceeds 95%**, record this information for [**Sev2 Incident creation**](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished.
    - **if no thresholds exceed 95%**, proceed to step 18.
- **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 18.

18. Select the **MySQL slow queries - total execution + locked time (seconds)** graph.

19. Check that queries do not exceed 1000 milliseconds:
- **During daily check:**
    - **if queries exceed 1000 milliseconds**, record this information for [**Sev2 Incident creation**](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished.
    - **if queries do NOT exceed 1000 milliseconds**, proceed to step 20.
- **During the alert investigation:** Make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to incident categorization as described in article [**[L1] Ticket Processing**](https://kb.epam.com/spaces/XBOXAOE/pages/2590766755/L1+Ticket+Processing).
[Screenshot with issue](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2018.png)
[Screenshot without issues](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2019.png)

20. **If necessary**, repeat the investigation process (steps 1–19) for the next cluster.
21. **Once the checks for all clusters are complete**, proceed to the next check.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYzOTgxMTc2MiwtNTgyODUyODQ1LDI4Nj
k1NTIxMywxOTYwOTQ3NTUxLC0yMDUzNTQwNzcyLC01MDEyNTcw
NTQsLTE2MzQyNDk5ODFdfQ==
-->