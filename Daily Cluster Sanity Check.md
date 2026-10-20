
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
|8. Select the **App Gateway - Responses by Status** graph.<br>9. Double-click on the graph to zoom in.<br>10. Set the time range to **[Past hour](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2049.png)** for investigating alerts.<br>11. Check the number of **4xx** and **5xx** errors detected and act accordingly:<br><br>&bull;**During daily check:**<br>&bull; **if fewer than 3,500 4xx errors AND fewer than 250 5xx errors**, proceed to step 12.<br>&bull; **if more than **3,500 4xx errors per sample (1 minute)**, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the Checks are finished.  Then proceed to step 12.<br>&bull; **if more than **250 5xx errors per sample (1 minute)**, record this information for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the Checks are finished. Then proceed to step 12.<br><br>&bull;**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 12. |<br>[More than 3,500 4xx errors per one sample (1 minute)](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2010.png) | [The graph without zoom](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2011.png)<br>[The graph zoomed by double-click](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2012.png) |
| 12. Select the **Lobby server VMs - CPU usage** graph.<br>13. Check the thresholds on the graph and act accordingly:<br><br>&bull;**During daily check:**<br>&bull; **if no threshold exceeds **70%**, proceed to step 14.<br>&bull; **if any threshold exceeds 70%**, record this information for **[Sev1 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all the checks are finished. Then proceed to step 14. <br><br>**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 14. |[The threshold exceeds 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2013.png) |[No thresholds exceed 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2014.png) |
| 14. Select the **Battle VMs - CPU usage** graph.<br>15. Check the thresholds on the graph and act accordingly:<br><br>&bull;**During daily check:**<br>&bull;**if any threshold exceeds 70%**,record for **[Sev1 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull;**if no threshold exceeds 70%**, proceed to step 16.<br><br>&bull;**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 16. | — | [No thresholds exceed 70%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2016.png) |
| 16. Select the **FlexibleDB/MySQL - CPU/Memory/Storage** graph.<br>17. Check the usage thresholds:<br>&bull;**During daily check:**<br>&bull; **if any threshold exceeds 95%**, record this information for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull; **if no threshold exceeds 95%**, proceed to step 18.<br><br>**During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 18. | — |[No thresholds exceed 95%](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2017.png) |
| 18. Select the **MySQL slow queries - total execution + locked time (seconds)** graph.<br>19. Check that queries do not exceed 1000 milliseconds:<br>&bull;**During daily check:**<br>&bull; **if queries exceed 1000 milliseconds** → record for **[Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation)** after all checks finish.<br>&bull; **if queries do NOT exceed 1000 ms**, proceed to step 20.<br><br>**&bull;During the alert investigation:** take a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to incident categorization as described in article [[L1] Ticket Processing](https://kb.epam.com/spaces/XBOXAOE/pages/2590766755/L1+Ticket+Processing). | [MySQL slow queries exceeds 1000 milliseconds](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2018.png) | [MySQL slow queries do NOT exceed 1000 ms](https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2019.png) |
|20. **If necessary**, repeat the investigation process (steps 1–19) for the next cluster.<br>21. **Once the checks for all clusters are complete**, proceed to the next Check. | — | — |

#### Test Client Check
> **NOTE!**
> Before the 1st check, ensure that the Test Client application was >downloaded as described in article **XBOX-AOE: Team onboarding** → tab *Guide for L1 Agent* → action *Configure Test Client*.
>
>The Test Plan Check during the **Daily Cluster Check** is performed for the following clusters:
>- aoelive
>- arthurlive
>- mythlive
>- tournament
>For **alert investigation**, the following clusters are checked:
>- aoelive
>- arthurlive
>- mythlive
>- tournament
>- aoeflight
>- aoetest

1. **For the Test Client Check**, open the folder on your laptop where the Test Client is stored: (e.g., `TestClient_Win_Feb22`).
(https://github.com/mikhailvorobev812/xbox/blob/main/xbox%20ss%2020.png)
2. Right-click on the **TestClientConfig.json** file icon and select **Edit with Notepad**.
3. Copy the code and replace the entire content of the file based on the cluster:

> **NOTE!** Blank spaces and indentations are important.

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
6. Press the **Enter** button. 
7. In the displayed command prompt, enter the command for the appropriate cluster:

Cluster

Command

aoeflight

`.\TestClient_Win.exe -server aoeflight.worldsedgelink.com`

aoelive

`.\TestClient_Win.exe -server aoe-api.worldsedgelink.com`

aoetest

`.\TestClient_Win.exe -server aoetest.worldsedgelink.com`

arthurlive

`.\TestClient_Win.exe -server arthurlive.worldsedgelink.com`

mythlive

`.\TestClient_Win.exe -server mythlive.worldsedgelink.com`

tournament

`.\TestClient_Win.exe -server ci6nbk4m67-api.worldsedgelink.com`

**8.** Press **Enter**. **9.** Once the home page is displayed, click the **Profile** tab.

> **IMPORTANT!** The test client check is an important indicator. If it does not work correctly, it might indicate a critical issue. Immediately create a new incident as described in article **[L1] ADO Ticket Creation**, escalate it as described in article **[L1] Major Incident & MIM Process**, and complete investigation steps afterwards.

**10.** Click the **Platform Login** button. **11.** Fill in the **Username** and **Password** with appropriate credentials depending on the cluster, stored in the **CyberArk portal**. **12.** Click the **Login** button. **13.** Wait for the authentication to complete and act accordingly:

-   **During daily check:**
    
    -   If authentication takes **≤30 sec** → record for the report (_Login < 30 sec_) and proceed to step 14.
        
    -   If authentication takes **>30 sec but <3 min** → post the following message into the **EPAM support channel** in MS Teams and follow instructions. Meanwhile, record for the report (_Login XX sec_) and proceed to step 14.
        
        > @everyone, hi team! The authentication during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
    -   If authentication takes **>3 min or fails** → record for the report (_Login >3 min_) and **Sev2 Incident creation** after all checks are finished. Then proceed to step 14.
        
        > **NOTE!** Monitor the right-hand Status panel. Actions are queued and removed as they are carried out. If there is no activity on this panel for 3 minutes, a ticket should be raised with **Sev1**.
        
-   **During the alert investigation:** record this information for the report (_Login XX_) and proceed to step 14.
    

**14.** Check the server in the status panel on the right to ensure you are logged into the correct server. **15.** Click the **Play** tab. **16.** Click the **Host** tab. **17.** Click **OK**. **18.** Wait for the connection to the Lobby game to be established and act accordingly:

-   **During daily check:**
    
    -   **≤30 sec** → record (_Battle Servers - Host Game < 30 sec_), proceed to step 19.
        
    -   **>30 sec but <3 min** → post message to **EPAM support channel** in MS Teams:
        
        > @everyone, hi team! The connection to Lobby game during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
        Record (_Battle Servers - Host Game XX_), proceed to step 19.
        
    -   **>3 min or fails** → record (_Battle Servers - Host Game >3 min_) and **Sev2 Incident creation** after all checks finish, then proceed to step 19.
        
        > **NOTE!** Monitor the Status panel; if no activity for 3 minutes, raise a ticket with **Sev1**.
        
-   **During the alert investigation:** record (_Battle Servers - Host Game XX_), proceed to step 19.
    

**19.** From the **Slots** drop-down menu, in the first slot select **AI**. **20.** Click the **Ready** button. **21.** Wait for the new screen to load and act depending on the loading time:

> FYI: Once the next screen is displayed, the virtual in-game action and test are successful.

-   **During daily check:**
    -   **≤30 sec** → record (_Battle Servers - Load into game < 30 sec_), proceed to step 22.
        
    -   **>30 sec but <3 min** → post to **EPAM support channel**:
        
        > @everyone, hi team! The creation of the game during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
        Record (_Battle Servers - Load into game XX sec_), proceed to step 22.
        
    -   **>3 min or fails** → record (_Battle Servers - Load into game >3 min / failed_) and **Sev2 Incident creation** after all checks finish, proceed to step 22.
        
-   **During the alert investigation:** record (_Battle Servers - Load into game XX_), proceed to step 22.

**22.** On the displayed page, select any button to complete the game (_a disconnecting screen is displayed_). **23.** Wait for game completion and act depending on time:

-   **During daily check:**
    
    -   **≤30 sec** → record (_Battle Servers - Completing a game < 30 sec_), proceed to step 24.
        
    -   **>30 sec but <3 min** → post to **EPAM support channel**:
        
        > @everyone, hi team! The completion of the game during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
        Record (_Battle Servers - Completing a game XX sec_), proceed to step 24.
        
    -   **>3 min or fails** → record (_Battle Servers - Completing a game >3 min / failed_) and **Sev2 Incident creation** after all checks finish, proceed to step 24.
        
        > **NOTE!** Monitor the Status panel; if no activity for 3 minutes, raise a ticket with **Sev1**.
        
-   **During the alert investigation:** record (_Battle Servers - Completing a game XX_), proceed to step 24.
    

**24.** In the **Party** tab, click **Create Party**. **25.** Wait for the lobby slots to become active and act depending on waiting time:

-   **During daily check:**
    -   **≤30 sec** → record (_Lobby Servers - Create Party < 30 sec_), proceed to step 26.
        
    -   **>30 sec but <3 min** → post to **EPAM support channel**:
        
        > @everyone, hi team! The party creation during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
        Record (_Lobby Servers - Create Party XX sec_), proceed to step 26.
        
    -   **>3 min or fails** → record (_Lobby Servers - Create Party >3 min / failed_) and **Sev2 Incident creation** after all checks finish, proceed to step 26.
        
-   **During the alert investigation:** record (_Lobby Servers - Create Party XX_), proceed to step 26.

**26.** Click **Leave Party**. **27.** Click the **Chat** tab. **28.** Select one of the **Available Channels**. **29.** Click **Join**. **30.** Confirm you successfully joined the channel (**Channel** and **Joined** sections). **31.** Write a test message in the text box. **32.** Click **Send**. **33.** Wait for the message to be displayed in the **Channel** section (test successful) and act depending on waiting time:

-   **During daily check:**
    
    -   **≤30 sec** → record (_Chat check successful_), proceed to step 34.
        
    -   **>30 sec but <3 min** → post to **EPAM support channel**:
        
        > @everyone, hi team! The communication with the chat during the cluster check for _name of the cluster_ takes approximately ** seconds. Please advise if any actions are needed from the L1 team?
        
        Record (_Chat check XX_), proceed to step 34.
        
    -   **>3 min or fails** → record (_Chat check >3 min / failed_) and **Sev2 Incident creation** after all checks finish, proceed to step 34.
        
        > **NOTE!** Monitor the Status panel; if no activity for 3 minutes, raise a ticket with **Sev1**.
        
-   **During the alert investigation:** record (_Chat check XX_) and proceed with **Cluster Check**.
    

**34.** Once the checks for test client are complete, proceed to the next check.

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

-   For Classic Outlook: `XBOX-AOE_Daily_Cluster_Sanity_Check_Report.msg`
-   For New Outlook: `XBOX-AOE_Daily_Cluster_Sanity_Check_Report.eml`

_Click here to expand the "no issues" template_

Field

Value

FROM

[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)

TO

[edge_link@microsoft.com](mailto:edge_link@microsoft.com);

CC

[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)

Subject

XBOX-AOE: Daily Cluster Sanity Check 1:00 AM/PM

Message

Hello Team,  
  
We have performed our Sanity Check for the following Clusters:  
• aoelive  
• arthurlive  
• mythlive  
• tournament  
  
**Test Plan AoeLive Cluster Check.**  
• Login < 30 sec  
• Lobby Servers - Create Party < 30 sec  
• Battle Servers - Host Game < 30 sec  
• Battle Servers - Load into game < 30 sec  
• Battle Servers - Completing a game < 30 sec  
• Chat check successful  
  
**Test Plan Arthurlive Cluster Check.**  
_(same 6 bullet points as above)_  
  
**Test Plan Mythlive Cluster Check.**  
_(same 6 bullet points as above)_  
  
**Test Plan Tournament Cluster Check.**  
_(same 6 bullet points as above)_  
  
Leader Board Test Were Successful  
  
Azure Service Health  
_Attach screenshot from Service Health_  
  
Best regards,  
_Epam signature_

#### B) If any issues were found

Make sure an ADO ticket is created as described in article **[L1] ADO Ticket Creation** (→ tab _Ticket for Cluster Check_).

Send the following report using mail template: `XBOX-AOE_Daily_Cluster_Sanity_Check_Report_issue_detected.msg`

_Click here to expand the email details_

Field

Value

FROM

[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)

TO

[edge_link@microsoft.com](mailto:edge_link@microsoft.com);

CC

[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)

Subject

XBOX-AOE: Daily Cluster Sanity Check 1:00 AM/PM

Message

Hello Team,  
  
We have performed our Sanity Check for the following Clusters:  
• aoeflight  
• aoelive  
• arthurlive  
• mythlive  
  
_An issue was identified on Cluster xxxx on Board xxxx. The following ticket was created xxxx._  
_Attach Screenshot of the issue(s) identified_  
  
**Test Plan AoeLive Cluster Check.**  
• Login < 30 sec / XX sec / >3 min / failed  
• Lobby Servers - Create Party < 30 sec / XX sec / >3 min / failed  
• Battle Servers - Host Game < 30 sec / XX sec / >3 min / failed  
• Battle Servers - Load into game < 30 sec / XX sec / >3 min / failed  
• Battle Servers - Completing a game < 30 sec / XX sec / >3 min / failed  
• Chat check successful / XX sec / >3 min / failed  
  
**Test Plan Arthurlive Cluster Check.**  
_(same pattern as above)_  
  
**Test Plan Mythlive Cluster Check.**  
_(same pattern as above)_  
  
**Test Plan Tournament Cluster Check.**  
_(same pattern as above)_  
  
**Leader Board Test Were Successful / Failed**  
  
**Azure Service Health**  
_Attach screenshot from Service Health_  
  
Best regards,  
_Epam signature_

----------

### Alert investigation

> ℹ️ Alert-investigation-specific instructions are embedded inline within each check above (look for the **"During the alert investigation"** bullet points under Cluster check, Test Client Check, Leader Board Check, and Azure Service Health). No separate standalone procedure was provided in the source beyond those inline branches.

```

A few notes on this conversion:
- I flagged a couple of source typos I noticed (e.g., "Test Cluster Check" vs. "Test Client Check" used inconsistently in the ordering list on page 3, and a stray "750px1000" artifact in the 4xx/5xx error step on page 8) — I kept the text as-is but happy to clean those up too if you want.
- Screenshots are referenced as `*(screenshot)*` placeholders since images can't be embedded directly in text-only Markdown here — I can add `![alt](path)` placeholders if you'll be dropping in actual image files.

Want me to (a) output this as a downloadable `.md` file, (b) also list out the typos/inconsistencies I spotted (like in the previous doc), or (c) merge this with the earlier LAPP-SACC markdown into one knowledge base file?

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzExNjQ4MzkzLC01ODc3NTI3NTQsMTk3MD
I5OTU0NCwxNTAxMjgwNTU2LC0xMTQ5MjA1Njk4LDU4MjI2ODg2
MCwtMjEwNjIxNTkyNCw3Nzc0NzM4MTQsLTE4OTAzMTQ5MTgsND
U0OTk3NDY2LDE0NDAzMzkwOSwtMTgxODE0MjE3NCwxNjA0MDky
MTU4LDIwMTcyNzI4OTAsLTQ3MDA2NDYyLC02MzA1NDM1MTgsMz
kxMjkxODc0LC01NzQxMjIzMTMsMTYyNzMxNzI5OCwtMjA1MTY0
MzIxNF19
-->