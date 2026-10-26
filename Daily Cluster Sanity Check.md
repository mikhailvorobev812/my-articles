
# [L1] Daily Cluster Sanity Check

[[_TOC_]]

## General information
**Concurrent Users (CCU)** is the number of people actively connected to a cluster at the same time. This metric is important to understand because it tells us about player load and potential performance impact.

|  | Preprod Clusters (AOETest, AOEFlight) | Prod Clusters (AOELive, Arthurlive, MYTHLive) |
|---|---|---|
| **Who connects** | Only Developers and EdgeLink Members. | Thousands of real players around the globe. |
| **Player activity** | No players are connected here. | Live gameplay sessions happen here. |
| **Impact** | ✅ There will **never** be CCU impact in Preprod because these clusters are not exposed to large-scale player activity. | ⚠️ CCU impact is **only relevant in Prod**, since load can affect stability, latency, and matchmaking. |
| **Example** | If AOETest shows a CCU of 5, that simply means a handful of developers are connected. This does not reflect real player traffic. | **Scenarios of CCU Impact in Prod:**<br><br>1. **High CCU (e.g., 50,000+ concurrent players)**<br>   - Matchmaking times may increase.<br>   - Servers may experience higher CPU/memory usage.<br>   - Some regions could see delays or instability.<br><br>2. **Sudden Spike in CCU (e.g., post-update or event launch)**<br>   - Logins may temporarily fail or slow down.<br>   - Backend services (auth, inventory, etc.) can become bottlenecks.<br><br>3. **Low CCU (e.g., during maintenance or downtime)**<br>   - Fewer reports from players.<br>   - Easier to run hotfix validations and monitoring checks. |
| **Screenshot** |(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%201.jpg) |(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%202.jpg)  |


>⚠️ **NOTE!**
The Daily Cluster Sanity Check should be performed  **daily (including weekends) at 3:00 AM CDT and 3:00  PM CDT / 2:00 AM CST and 2:00 PM CST**  
(for other time zones,follow the link to the  [time converter](https://www.worldtimebuddy.com/?pl=1&lid=306,30,611717,625144,314,312,206,0,212&h=306&hf=0), or as part of an alert investigation.

## Daily Cluster Sanity Check
### 1. Performing Checks
Within the Daily Cluster Sanity Check, perform **all 4 checks** in the following order:

1. [Cluster check](#cluster-check)
2. [Test Client Check](#test-client-check)
3. [Leader Board Check](#leader-board-check)
4. [Azure Service Health](#azure-service-health)

For alert investigation, perform only **2 checks** in the following order:

1.  [Test Client Check](#test-client-check)
2.  [Cluster check](#cluster-check)

#### Cluster check
| Actions | Screenshots with issues | Screenshots without issues |
|---|---|---|
|1. For **Cluster Check**, open the Cluster's Dashboard by clicking an appropriate link from the list below depending on the type of check/investigation:<br><br>**⚠️IMPORTANT!**<br>To perform the **Daily Cluster Sanity Check**, the following clusters should be checked:<br>&bull;**aoelive**<br>&bull;**arthurlive**<br>&bull;**mythlive**<br>For alert investigation, only the **cluster mentioned in the alert** notification should be checked.<br><br> For daily cluster check: <br>&bull;aoelive → [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard) <br>&bull;arthurlive → [Arthurlive Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/arthurlive-tf-rsg/providers/microsoft.portal/dashboards/arthurlive-monitoring-dashboard) <br>&bull;mythlive → [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)<br><br>For daily cluster check: <br>&bull;aoeflight → [AOE FLIGHT Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoeflight-tf-rsg/providers/Microsoft.Portal/dashboards/aoeflight-monitoring-dashboard) <br>&bull;aoelive → [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard) <br>&bull;aoetest → [AOE TEST Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoetest-tf-rsg/providers/Microsoft.Portal/dashboards/aoetest-monitoring-dashboard) <br>&bull;mythlive → [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)| — | — |
| 2. Set the time range to **Past hour** for investigating alerts:<br>[Set time range to Past hour](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2049.png) | — | — |
| ⚠️**IMPORTANT!**<br>**Lobby - Total CCU on the cluster** graph is a critical indicator. If any gaps or drops are identified, it might indicate a CCU impact issue.<br>Immediately create a new incident as described in article [[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation). Escalate it as described in article [[L1] Major Incident & MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) and complete investigation steps afterward.<br><br> 3. Select the **Lobby - Total CCU on cluster** graph.<br> 4. Double-click on the graph to zoom in.<br> 5. Check if there are any gaps or drops and act accordingly: <br><br>&bull; **During daily EU/APAC check:**<br> &bull; **if there fewer then 5 missing points or no missing points**, proceed to step 6.<br> &bull;**if there are 6 or more missing points gap/a significant drops**, record this information for [**Sev1** **Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) and proceed to step 6.<br><br>**During daily MX check:**<br> &bull; **if fewer than 5 missing points or no missing points** → proceed to step 6.<br> &bull; **if 6+ missing points / a significant drop → ask L2/L3 on the **[EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47)** in MS Teams to confirm if a ticket is needed, follow instructions. Meanwhile, proceed to step 6.<br>```@everyone, hi team!<br>> During the cluster check, we found a 5-point gap on *name of the cluster*.<br>> Please advise if any actions are needed from the L1 team<br>```<br>**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Then proceed to step 6. | **The graph with significant drop:**<br>[CCU graph with drop](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%203.png) **<br>[CCU graph with significant drop](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%204.png)<br><br>**The gap with 6 missing points:[CCU graph with 6-point gap circled](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%205.png) | **The graph without gaps:**<br>[CCU graph without gaps](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%206.png)<br><br>**The graph zoomed by double-click:**<br>[CCU graph zoomed](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%207.png) |
|6. Select the **App Gateway - Backends health (below: unhealthy only)** graph.<br>7. Check **Unhealthy Backend amount**:<br>&bull;**During daily check:**<br> &bull; **if Unhealthy Backend is lower than 0.75** proceed to step 8.<br>&bull; **if Unhealthy Backend is higher than 0.75** → record for **[Sev2 Incident creation]**(https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all checks finish. Then proceed to step 8.<br>&bull; **if an Unhealthy backend that later recovered was identified**, add a comment about that in [the e-mail report about the check results](https://kb.epam.com/spaces/XBOXAOE/pages/2702409893/L1+Daily+Cluster+Sanity+Check#id-[L1]DailyClusterSanityCheck-DailyCheckResults). Take a screenshot and attach it as proof to the e-mail report as well. Then proceed to step 8.<br><br>&bull;**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 8. | <br>[Unhealthy Backend is higher than 0.75](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%208.png) | <br>[Unhealthy Backend is lower than 0.75](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%209.png) |
|8. Select the **App Gateway - Responses by Status** graph.<br>9. Double-click on the graph to zoom in.<br>10. Set the time range to **[Past hour](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2049.png)** for investigating alerts.<br>11. Check the number of **4xx** and **5xx** errors detected and act accordingly:<br><br>&bull;**During daily check:**<br>&bull; **if fewer than 3,500 4xx errors AND fewer than 250 5xx errors**, proceed to step 12.<br>&bull; **if more than 3,500 4xx errors per sample (1 minute)**, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished.  Then proceed to step 12.<br>&bull; **if more than 250 5xx errors per sample (1 minute)**, record this information for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the Checks are finished. Then proceed to step 12.<br><br>&bull;**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 12. |<br>[More than 3,500 4xx errors per one sample (1 minute)](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2010.png) | [The graph without zoom](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2011.png)<br>[The graph zoomed by double-click](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2012.png) |
| 12. Select the **Lobby server VMs - CPU usage** graph.<br>13. Check the thresholds on the graph and act accordingly:<br><br>&bull;**During daily check:**<br>&bull; **if no threshold exceeds 70%**, proceed to step 14.<br>&bull; **if any threshold exceeds 70%**, record this information for **[Sev1 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the checks are finished. Then proceed to step 14. <br><br>**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 14. |[The threshold exceeds 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2013.png) |[No thresholds exceed 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2014.png) |
| 14. Select the **Battle VMs - CPU usage** graph.<br>15. Check the thresholds on the graph and act accordingly:<br><br>&bull;**During daily check:**<br>&bull;**if any threshold exceeds 70%**,record for **[Sev1 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull;**if no threshold exceeds 70%**, proceed to step 16.<br><br>&bull;**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 16. | — | [No thresholds exceed 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2016.png) |
| 16. Select the **FlexibleDB/MySQL - CPU/Memory/Storage** graph.<br>17. Check the usage thresholds:<br>&bull;**During daily check:**<br>&bull; **if any threshold exceeds 95%**, record this information for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull; **if no threshold exceeds 95%**, proceed to step 18.<br><br>**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 18. | — |[No thresholds exceed 95%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2017.png) |
| 18. Select the **MySQL slow queries - total execution + locked time (seconds)** graph.<br>19. Check that queries do not exceed 1000 milliseconds:<br>&bull;**During daily check:**<br>&bull; **if queries exceed 1000 milliseconds** → record for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull; **if queries do NOT exceed 1000 ms**, proceed to step 20.<br><br>**&bull;During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to incident categorization as described in article [[L1] Ticket Processing](https://kb.epam.com/spaces/XBOXAOE/pages/2590766755/L1+Ticket+Processing). | [MySQL slow queries exceeds 1000 milliseconds](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2018.png) | [MySQL slow queries do NOT exceed 1000 ms](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2019.png) |
|20. **If necessary**, repeat the investigation process (steps 1–19) for the next cluster.<br>21. **Once the checks for all clusters are complete**, proceed to the next Check. | — | — |

#### Test Client Check
> ⚠️**NOTE!**
> Before the 1st check, ensure that the Test Client application was >downloaded as described in article **XBOX-AOE: Team onboarding** → tab *Guide for L1 Agent* → action *Configure Test Client*.
>
>The Test Plan Check during the **Daily Cluster Check** is performed for the following clusters:
>- **aoelive**
>- **arthurlive**
>- **mythlive**
>- **tournament**
>For **alert investigation**, the following clusters are checked:
>- **aoelive**
>- **arthurlive**
>- **mythlive**
>- **tournament**
>- **aoeflight**
>- **aoetest**

1. **For the Test Client Check**, open the folder on your laptop where the Test Client is stored: (e.g., `TestClient_Win_Feb22`).
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2020.png)
2. Right-click on the **TestClientConfig.json** file icon and select **Edit with Notepad**.
3. Copy the code and replace the entire content of the file based on the cluster:

> ⚠️**NOTE!** 
> Blank spaces and indentations are important.

**Cluster:** `mythlive`
```json
    "titleID": 5,
    "name": "elink",
    "majorVersion": "4.0.0",
    "minorVersion": 0,
    "simPeriodSeconds": 0.125,
    "defaultServer": "aoe"
```

**Cluster:** `aoelive`, `arthurlive`, `aoeflight`, `aoetest`, `tournament`

```json
    "titleID": 2,
    "name": "rlink",
    "majorVersion": "4.0.0",
    "minorVersion": 0,
    "simPeriodSeconds": 0.125,
    "defaultServer": "aoe"
```
4. Save the changes and close the file. 
5. In the directory path, type the command `powershell`. 
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2021.png)
6. Press the **Enter** button. 
7. In the displayed command prompt, enter the command for the appropriate cluster:

| Cluster | Command |
|---|---|
| **aoeflight** | `.\TestClient_Win.exe -server aoeflight.worldsedgelink.com`|
| **aoelive** | `.\TestClient_Win.exe -server aoe-api.worldsedgelink.com` |
| **aoetest** |`.\TestClient_Win.exe -server aoetest.worldsedgelink.com`|
| **arthurlive** |`.\TestClient_Win.exe -server arthurlive.worldsedgelink.com`|
| **mythlive** |`.\TestClient_Win.exe -server mythlive.worldsedgelink.com`|
| **tournament** |`.\TestClient_Win.exe -server ci6nbk4m67-api.worldsedgelink.com`|
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2022.png)
8. Press the **Enter** button.
9. Once the home page is displayed, click the **Profile** tab.

> **⚠️IMPORTANT!** The test client check is an important indicator. If it does not work correctly, it might indicate a critical issue. Immediately create a new incident as described in article **[[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)**, escalate it as described in article **[[L1] Major Incident & MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process)**, and complete investigation steps afterwards.

10. Click the **Platform Login** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2023.png)
11. Fill in the **Username** and **Password** with appropriate credentials depending on the cluster stored in [1Password](https://epam.1password.com/).
12. Click the **Login** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2024.png)
13.  Wait for the authentication to complete and act accordingly:
-   **During daily check:**
    
    -   **if authentication takes 30 seconds or less**, record this information for the report (_Login < 30 sec_) and proceed to step 14.
       -   **if authentication** **takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the provided instructions. Meanwhile, record this information for the report (_Login XX sec_) and proceed to step 14.
        > @everyone, hi team! The authentication during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
    -   **if authentication takes** **more than 3 minutes or fails**, record this information for the report (_Login >3 min_) and  [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 14.
        
        > **⚠️NOTE!** Monitor the right-hand Status panel. Actions are queued and removed as they are carried out. If there is no activity on this panel for 3 minutes, a ticket should be raised with **Sev1**.
        
-   **During the alert investigation:** record this information for the report (_Login XX_) and proceed to step 14.

14. Check the server in the status panel on the right to ensure you are logged into the correct server:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2025.png)
15. Click the **Play** tab: 
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2026.png)
16. Click the **Host** tab: 
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2027.png)
17. Click **OK**: 
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2028.png)
18. Wait for the connection to Lobby game to be established and act accordingly:
   -   **During daily check:**
        -   **if connection to Lobby game takes up to 30 sec**, record this information for the report (_Battle Servers - Host Game < 30 sec_) and proceed to step 19.
        -   **if connection to Lobby game takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the instructions. Meanwhile, record this information for the report (_Battle Servers - Host Game XX_) and proceed to step 19.
        
        > @everyone, hi team! The connection to Lobby game during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
       -   **if connection to Lobby game takes more than 3 minutes or fails**, record this information for the report (_Battle Servers - Host Game >3 min_) and  [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 19.
        
        > **⚠️NOTE!** Monitor the Status panel; if no activity for 3 minutes, raise a ticket with **Sev1**.
        
-   **During the alert investigation:** record (_Battle Servers - Host Game XX_), proceed to step 19.

19.  On the appeared menu from the **Slots** drop-down menu, in the first slot select **AI**:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2029.png)
20.  Click the **Ready** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2030.png)
21. Wait for the new screen to be loaded and act depending on the loading time:

> **FYI:**
>  Once the next screen is displayed, the virtual in-game action and test are successful.
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2031.png)
-   **During daily check:**
    -   **if the creation of the game takes up to 30 sec**, record this information for the report (_Battle Servers - Load into game < 30 sec_) and proceed to step 22.
    -   **if the creation of the game takes** **more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the instructions. Meanwhile, record this information for the report (_Battle Servers - Load into game XX sec_) and proceed to step 22.
        
        > @everyone, hi team! 
        The creation of the game during the cluster check for _name of the cluster_ takes approximately ** seconds. 
        Please advise if any actions are needed from the L1 team?
                
    -  **if the creation of the game takes** **more than 3 minutes or fails**, record this information for the report (_Battle Servers - Load into game >3 min / failed_) and [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 22.  
           
-   **During the alert investigation**, record this information for the report (_Battle Servers - Load into game XX_) and proceed to step 22.

22. On the displayed page, select any button to complete the game:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2032.png)

> **FYI:** A disconnecting screen is displayed.
[Disconnecting screen](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2033.png)
23. Wait for the game completion and act depending on the time it takes:
   -   **During daily check:**
        -   **if the game completion takes** **up to 30 sec**, record this information for the report (_Battle Servers - Completing a game < 30 sec_) and proceed to step 24.
        -   **if the game completion takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the provided instructions. Meanwhile, record this information for the report (_Battle Servers - Completing a game XX sec_) proceed to step 24.
        
        > @everyone, hi team! The completion of the game during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
       -   **if the game completion takes** **more than 3 minutes or fails**, record this information for the report (_Battle Servers - Completing a game >3 min / failed)_ and [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)  after all the Checks are finished. Then proceed to step 24.
        
        > **⚠️NOTE!** Monitor the right-hand side **Status** panel. If there is no activity on this panel for 3 minutes, a ticket should be raised with Sev1
-   **During the alert investigation,** record this information for the report (_Battle Servers - Completing a game XX)_ and  proceed to step 24.
    
24. In the **Party** tab, click the **Create Party** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2034.png)
25.  Wait for the lobby slots to become active and act depending on the waiting time:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2035.png)
-   **During daily check:**
    -   **if the party creation takes up to 30 sec**, record this information for the report (_Lobby Servers - Create Party < 30 sec_) and proceed to step 26.
    -   **if the party creation takes** **more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the instructions. Meanwhile, record this information for the report (_Lobby Servers - Create Party XX sec_) and proceed to step 26.
        
        > @everyone, hi team! 
        The party creation during the cluster check for _name of the cluster_ takes approximately ** seconds. 
        Please advise if any actions are needed from the L1 team?
        
       -   **if the party creation takes more than 3 minutes or fails**, record this information for the report (_Lobby Servers - Create Party >3 min / failed_) and [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 26.
-   **During the alert investigation:** record this information for the report (_Lobby Servers - Create Party XX_) and proceed to step 26.

26. Click the **Leave Party** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2036.png)
27. Click the **Chat** tab.
28.  Select one of the **Available Channels**.
29.  Click the **Join** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2037.jpg)
30. Check that you successfully join the channel in the **Channel**  and  **Joined sections**:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2038.png)
31.  Write a test message in the text box.
32.  Click **Send** button:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2039.jpg)
33. Wait for the message to be displayed in the **Channe**l section (i.e., the test is successful) and act depending on the waiting time:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2040.png)
-   **During daily check:**
    -   **if the communication with the Chat takes** **up to 30 sec**, record this information for the report (_Chat check successful_) and proceed to step 34.
    -   **if the communication with the Chat takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the instructions. Meanwhile, record this information for the report (_Chat check XX_) and proceed to step 34.
        
        > @everyone, hi team! 
        The communication with the chat during the cluster check for _name of the cluster_ takes approximately ** seconds. 
        Please advise if any actions are needed from the L1 team?
        
    -  **if the communication with the Chat takes** **more than 3 minutes or fails**, record this information for the report (_Chat check >3 min / failed_) and [**Sev2 Incident** creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 34.
        
        > **⚠️NOTE!** 
        Monitor the right-hand side **Status** panel. Actions are queued and removed as they are carried out.
        
-    **During the alert investigation**, record this information for the report (_Chat check XX_) and proceed with Cluster Check.
    
34. Once the checks for test client are complete, proceed to the next check.

----------

### Leader Board Check
1.  **For Leader Board Check**, go to [AoE Live Leaderboard](https://aoe-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty). 
2. Check the result **message** and act accordingly:
&bull;  **if there is a `"SUCCESS"` status**, record for the report, proceed to step 3.
&bull;    **if there is another status**, record for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all checks finish, proceed to step 3.
[AoE Live Leaderboard with SUCCESS status](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2041.png)
3. Go to **[Myth Live Leaderboard](https://athens-live-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=athens&format=jsonpretty)**. 
4. Check the result **message** and act accordingly:
-  **if there is a part of code with SUCCESS status,** record this information for the report and proceed to step 5.
-   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 5.
[Myth Live Leaderboard with SUCCESS status](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2042.png)
5. Go to [AoE Flighting Leaderboard](https://flighting-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty).
6. Check the result **message** and act accordingly:  
  -   **if there is a part of code with SUCCESS status,** record this information for the report and  proceed to step 7.
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to step 7.
[AoE Flighting Leaderboard with SUCCESS status](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2043.png)
7. Go to [AoE Test Leaderboard](https://aoetest-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty).
8. Check the result **message** and act accordingly:  
  -   **if there is a part of code with SUCCESS status,** proceed to Azure Service Health check.
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to Azure Service Health check.
[AoE Test Leaderboard with SUCCESS status](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2044.png).
----------

### Azure Service Health

 1.  **For Azure Service Health** check go to [Azure Service Health](https://portal.azure.com/#view/Microsoft_Azure_Health/AzureHealthBrowseBlade/~/serviceIssues) page.
2.  Check the affected Locations (red location status) and act accordingly:
[**No affected locations**](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2045.png)
[**Affected locations detected**](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2046.png)
-   **if there are NO Affected locations** proceed to processing cluster check results.
-   **if there are** **Affected locations,** make a  screenshot of the dashboard and save it locally to be later uploaded and proceed to step 3.
3. Click on the **Issue name** link. 
[**Issue name**](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2047.png)
4. Make a  screenshot of the page and save it locally to be later uploaded into the related ADO ticket.
5. Copy the **issue name** and use it for naming when creating a [new Incident](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished:
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2048.png)
6. Proceed to [processing cluster check results](https://kb.epam.com/spaces/XBOXAOE/pages/2702409893/L1+Daily+Cluster+Sanity+Check#id-[L1]DailyClusterSanityCheck-DailyCheckResults) → tab _**Issues detected.**_

----------

## 2. Processing cluster check results

### Daily Cluster Sanity Check Results

Depending on the Daily Cluster Sanity Check results, proceed with the following steps:

#### A) If no issues were found

Send the following report using the mail template:

| From: | supportxbox-aoel1@epam.com |
|:------|:---------------------------|
| To: | edge_link@microsoft.com; |
| CC: | supportxbox-aoel1@epam.com |
| Subject: | XBOX-AOE: Daily Cluster Sanity Check 12:00 AM/PM |
| Body: | Hello Team,<br>We have performed our Sanity Check for the following Clusters:<br><br>* aoetest <br>* arthurlive <br>*    mythlive<br><br> **Test Plan _NAME OF CLUSTER_ Cluster Check.**<br><br>* Login < 30 sec<br>* Lobby Servers - Create Party  < 30 sec<br>* Battle Servers - Host Game  < 30 sec<br>* Battle Servers - Load into game < 30 sec<br>* Battle Servers - Completing a game < 30 sec<br>* Chat check successful<br><br>**Leader Board Test Were Successful.**<br><br>**Azure Service Health**<br><br><Attach Screenshot><br><br>Best regards, <br><br> Epam signature |

#### B) If any issues were found

1. Make sure an ADO ticket is created as described in article [[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation).
2. Whenever a ticket is created, add a justification in the **Comments** section of the ADO ticket explaining why the ticket is being created:
```ISSUE XXXXXX - ticket will be escalated to the L2 team.```
 > **⚠️NOTE!** Every created ticket must contain a justification comment. The comment must clearly state the identified issue and the planned action.
3. Post a message from **Microsoft (Guest)** account in  MS Teams in the **[Edgelink > EPAM support](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47)** channel:
```ISSUE XXXXXX -  TITLE  -  PRIORITY - @EPAM support```
Tickets without a comment or a justified investigation are considered incomplete.
4. Once the ADO Ticket has been created, select the relevant recipient from the table below:

| Conditions (cluster, issue type) | Send the email to (PagerDuty email) / ticket creation |
|---|---|
| **aoeflight** | R02NNFK5EX5QTQDE21R8PUS0ABGZMM@edgelink.pagerduty.com |
|**aoelive**, **Azure Service Health issue** | R02INFF2RJH6HCPZMXIPUVOXZENV@edgelink.pagerduty.com |
| **aoetest** | R028ECLXYL5UZSWBTXLWQGQ7783CJ@edgelink.pagerduty.com |
| **arthurlive** | R02BWPNQNYFBOOMALPMMAU51KVIDG@edgelink.pagerduty.com |
| **mythlive** | R02OKFXNB1QKD928PGM2D197879E@edgelink.pagerduty.com |
| **tournament** | R02J04J8Q71QK379D6LDTNG3T04S8@edgelink.pagerduty.com |


5. Send the following report using mail template:

| From: | supportxbox-aoel1@epam.com |
|:------|:---------------------------|
| To: | edge_link@microsoft.com; **Pagerduty email** |
| CC: | supportxbox-aoel1@epam.com |
| Subject: | Fired:Sev1/2/3  Azure Monitor Alert cluster - Issue Identified during Cluster Check |
| Body: | An issue was identified on Cluster xxxx on Board xxxx. The following ticket was created xxxx. <br>EPAM SIGNATURE |
6. Ensure that the notification for the PagerDuty alert is triggered within 10 minutes:
-   **if the PagerDuty incident is created automatically,** process the new PagerDuty Incident as described in article [[L1] Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2607572290/L1+Azure+Alerts+handling).
- **if the PagerDuty incident is NOT created automatically,** manually create  a new PagerDuty incident as described in article [[L1] PagerDuty ticket creation](https://kb.epam.com/spaces/XBOXAOE/pages/2581370814/L1+PagerDuty+ticket+creation). Then process the new PagerDuty Incident as described in article [[L1] Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2607572290/L1+Azure+Alerts+handling).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA3MjkwNzEwMSwtMTIyODAxNDQxLC00Mj
k0MzI0NDQsMTQ5MTY5ODcyNiwtNTc3NjI0OTIsNjkxOTg1MTI0
LC0yNjg1NzgzMSwtNjcyMDU4NTYwLC0xNTc2NzAzNzE4LC0yMD
czMzUxNTg2LC0xMzcxNjgyMjA3LC0yMDAzMjQ0MDEzLDExMzU1
OTQ1NDMsNDgwNDM1NTAyLDIwNzcxMDk3NDQsLTU5NDA2ODI0Ni
w0NDE5Nzg4MjAsMzExNjQ4MzkzLC01ODc3NTI3NTQsMTk3MDI5
OTU0NF19
-->