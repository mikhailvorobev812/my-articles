# [L1] Daily Cluster Sanity Check

## General information

**Concurrent Users (CCU)** is the number of people actively connected to a cluster at the same time. This metric is important to understand because it tells us about player load and potential performance impact.

### Preprod and production CCU

Aspect

Preprod Clusters (AOETest, AOEFlight)

Prod Clusters (AOELive, Arthurlive, MYTHLive)

Who connects

Only Developers and EdgeLink Members.

Thousands of real players around the globe.

Player activity

No players are connected here.

Live gameplay sessions happen here.

Impact

✅ There will never be CCU impact in Preprod because these clusters are not exposed to large-scale player activity.

⚠️ CCU impact is only relevant in Prod , since load can affect stability, latency, and matchmaking.

**Preprod example:** If AOETest shows a CCU of 5, that simply means a handful of developers are connected. This does not reflect real player traffic.** Production CCU impact scenarios:**

-   **High CCU (e.g., 50,000+ concurrent players):** Matchmaking times may increase; servers may experience higher CPU/memory usage; some regions could see delays or instability.
-   **Sudden CCU spike (e.g., after an update or event launch):** Logins may temporarily fail or slow down; backend services (auth, inventory, etc.) can become bottlenecks.
-   **Low CCU (e.g., during maintenance or downtime):** Fewer reports from players; easier to run hotfix validations and monitoring checks.** Cluster screenshots:**

![xbox AOEFlight.jpg](https://app.glean.com/chat/sanity_check_assets/xbox_AOEFlight.jpg)

![xbox AOElive prod.jpg](https://app.glean.com/chat/sanity_check_assets/xbox_AOElive_prod.jpg)

> **NOTE!**
> 
> The Daily Cluster Sanity Check should be performed **daily (including weekends) at 3:00 AM CDT and 3:00 PM CDT / 2:00 AM CST and 2:00 PM CST** (for other time zones, follow the link to the [time converter](https://www.worldtimebuddy.com/?pl=1&lid=306,30,611717,625144,314,312,206,0,212&h=306&hf=0)), or as part of an alert investigation.

## 1. Performing checks

Within the Daily Cluster Sanity Check perform all the 4 checks in the following order:

1.  [Cluster check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#cluster-check)
2.  [Test Cluster Check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#test-cluster-check)
3.  [Leader Board Check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#leader-board-check)
4.  [Azure Service Health](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#azure-service-health)

For alert investigation, perform only **2 checks** in the following order:

1.  [Test Cluster Check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#test-cluster-check)
2.  [Cluster check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#cluster-check)

### Cluster check

#### Cluster-check procedure

**Action:**

1.  For Cluster Check, open the Cluster's Dashboard by clicking an appropriate link from the list below depending on the type of check / investigation:

> **IMPORTANT!**
> 
> To perform the Daily Cluster Sanity Check, the following clusters should be checked:
> 
> -   **aoelive**
> -   **arthurlive**
> -   **mythlive**
> 
> For alert investigation, only the cluster mentioned in the alert notification should be checked.

**For daily cluster check:**

-   **aoelive**- [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard)
-   **arthurlive** - [Arthurlive-Monitoring-Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/arthurlive-tf-rsg/providers/microsoft.portal/dashboards/arthurlive-monitoring-dashboard)
-   **mythlive**- [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)

**For alert investigation:**

-   **aoeflight** - [AOE FLIGHT Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoeflight-tf-rsg/providers/Microsoft.Portal/dashboards/aoeflight-monitoring-dashboard)
-   **aoelive**- [AOE LIVE Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoelive-tf-rsg/providers/Microsoft.Portal/dashboards/aoelive-monitoring-dashboard)
-   **aoetest** - [AOE TEST Monitoring Dashboard](https://portal.azure.com/#dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourceGroups/aoetest-tf-rsg/providers/Microsoft.Portal/dashboards/aoetest-monitoring-dashboard)
-   **arthurlive** - [Arthurlive-Monitoring-Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/arthurlive-tf-rsg/providers/microsoft.portal/dashboards/arthurlive-monitoring-dashboard)
-   **mythlive**- [Myth Live Monitoring Dashboard](https://portal.azure.com/#@worldsedge.msgamestudios.com/dashboard/arm/subscriptions/a6591785-2ac3-4686-bd24-9519787c46a8/resourcegroups/mythlive-tf-rsg/providers/microsoft.portal/dashboards/mythlive-monitoring-dashboard)

**Action:**

2.  Set the time range to **Past hour** for investigating alerts:  
    ![image-2025-7-4_12-51-5.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-4_12-51-5.png)

**Action:**

> **IMPORTANT!**
> 
> **Loby - Total CCU on the cluster graph** is a critical indicator. If any gaps or drops are identified, it might indicate a CCU impact issue.
> 
> Immediately create a new incident as described in article [[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation). Escalate it as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) and complete investigation steps afterward.

3.  Select the **Lobby - Total CCU on cluster** graph.
4.  Double-click on the graph to zoom in.
5.  Check if there are any any gaps or drops and act accordingly:

-   **During daily EU/APAC check:**
    
    -   if there fewer then 5 missing points or no missing points, proceed to step 6.
    -   if there are 6 or more missing points gap/a significant drops, record this information for [Sev1 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) and proceed to step 6.
-   **During daily MX check:**
    
    -   if there fewer then 5 missing points or no missing points, proceed to step 6.
        
    -   **if there are 6 or more missing points gap/a significant drops,** ask L2/L3 on the [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams to confirm if a ticket is needed, and follow the instructions. Meanwhile, proceed to step 6.
        
        > **NOTE!**
        > 
        > @everyone, hi team!  
        > During the cluster check, we found a 5-point gap on name of the cluster.  
        > Please advise if any actions are needed from the L1 team
        
-   **During the alert investigation:** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Then proceed to step 6.** Screenshots / examples with issues:**
    

The graph with significant drop:  
![image-2025-6-30_17-23-4.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-23-4.png)![image-2025-7-9_17-4-8.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-9_17-4-8.png)  
The gap with 6 missing points:  
![image-2025-6-30_17-25-8.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-25-8.png)

**Screenshots / examples without issues:**

The graph without zoom:  
![image-2025-7-4_13-11-9.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-4_13-11-9.png)  
The graph zoomed by double-click:  
![image-2025-6-30_17-20-25.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-20-25.png)

**Action:**

6.  Select the **App Gateway - Backends health (below: unhealthy only)** graph.
    
7.  Check Unhealthy Backend amount:
    

-   **During daily check:**
    
    -   **if Unhealthy Backend lower than 0.75** proceed to step 8.
    -   if Unhealthy Backend is higher than 0.75, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 8.
    -   if an unhealthy backend that later recovered was identified, add a comment about that in [e-mail report about the check results](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#e-mail-report-about-the-check-results). Make a screenshot and attach it as a proof to the e-mail report as well. Then proceed to step 8.
-   **During the alert investigation:** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 8.
    

**Screenshots / examples with issues:**

Unhealthy Backend is higher than 0.75  
![image-2025-6-30_17-28-16.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-28-16.png)

**Screenshots / examples without issues:**

Unhealthy Backend is lower than 0.75

![image-2025-6-30_17-26-34.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-26-34.png)

**Action:**

8.  Select the **App Gateway - Responses by Status** graph.
    
9.  Double-click on the graph to zoom in.
    
10.  Set the time range to **Past hour** for investigating alerts:  
    ![image-2025-7-4_12-51-5.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-4_12-51-5.png)
    
11.  Check the number of 4xx and 5xx errors detected and act accordingly:
    

-   **During daily check:**
    
    -   **if there fewer than 3500 4xx errors AND fewer than 250 5xx errors,** proceed to step 11.
    -   if there are more than 3,500 4xx errors per sample (1 minute), record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 11.
    -   **if there are more than 250 5xx errors per sample (1 minute), record this information for [Sev2 Incidentcreation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 11.**
-   **During the alert investigation:** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 11.
    

**Screenshots / examples with issues:**

More than 3,500 4xx errors per one sample (1 minute)

![image-2026-7-9_16-37-46.png](https://app.glean.com/chat/sanity_check_assets/image-2026-7-9_16-37-46.png)

**Screenshots / examples without issues:**

The graph without zoom:  
![image-2025-7-4_15-17-31.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-4_15-17-31.png)  
The graph zoomed by double-click:

![image-2025-6-30_17-32-59.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-32-59.png)

**Action:**

12.  Select the **Lobby server VMs - CPU usage** graph.
    
13.  Check the thresholds on the graph and act accordingly:
    

-   **During daily check:**
    
    -   **if no thresholds exceeds 70%,** proceed to step 14.
    -   if any threshold exceeds 70%, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to step 13.
-   **During the alert investigation:** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 13.
    

**Screenshots / examples with issues:**

The threshold exceeds 70%

![image-2025-6-30_17-54-3.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-54-3.png)![image-2025-6-30_17-55-3.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-55-3.png)

**Screenshots / examples without issues:**

No thresholds exceed 70%

![image-2025-6-30_17-47-22.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-47-22.png)

**Action:**

14.  Select the **Battle VMs - CPU usage** graph.
    
15.  Check the the thresholds on the graph and act accordingly:
    

-   **During daily check**
    
    -   if any threshold exceeds 70%, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished.
    -   if no thresholds exceeds 70%, proceed to step 16.
-   **During the alert investigation:** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 15.
    

**Screenshots / examples without issues:**

No thresholds exceed 70%

![image-2025-6-30_17-48-26.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-48-26.png)

**Action:**

16. Select the **FlexibleDB/MySQL - CPU/Memory/Storage** graph.

17. Check the usage thresholds:

-   **During daily check:**
    
    -   if any threshold exceeds 95%, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished.
    -   if no thresholds exceeds 95%, proceed to step 18.
-   During the alert investigation, make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to step 17.
    

**Screenshots / examples without issues:**

No thresholds exceed 95%![image-2025-6-30_17-42-20.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_17-42-20.png)

**Action:**

18. Select the **MySQL slow queries - total execution + locked time (seconds)** graph.

19. Check that queries do not exceed 1000 milliseconds:

-   **During daily check:**
    
    -   if queries exceed 1000 milliseconds, record this information for [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished.
    -   if queries do NOT exceed 1000 milliseconds, proceed to step 20.
-   **During the alert investigation,** make a screenshot of the graph and save it locally to be later uploaded into the related ADO ticket. Proceed to incident categorization as descried in article [[L1] Ticket Processing](https://kb.epam.com/spaces/XBOXAOE/pages/2590766755/L1+Ticket+Processing).
    

**Screenshots / examples with issues:**

![image-2026-3-20_10-54-35.png](https://app.glean.com/chat/sanity_check_assets/image-2026-3-20_10-54-35.png)

**Screenshots / examples without issues:**

![Screenshot 2025-11-13 at 2.33.40 p.m..png](https://app.glean.com/chat/sanity_check_assets/Screenshot_2025-11-13_at_2.33.40_p.m..png)

**Action:**

20. If necessary, repeat the investigation process (step 1 - 19) for the next cluster.  
21. Once the checks for all clusters are complete, proceed to the next Check.

### Test Client Check

> **NOTE!**
> 
> **Before the 1st check** ensure that the Test Client application was downloaded as described in article [XBOX-AOE: Team onboarding](https://kb.epam.com/spaces/EPMGSD/pages/2308597138/XBOX-AOE+Team+onboarding) → tab_**Guide for L1 Agent**_ → action_**Configure Test Client.**_
> 
> The Test Plan Check during the **Daily Cluster Check** is performed for the following clusters:
> 
> -   **aoelive**
>     
> -   **arthurlive**
>     
> -   mythlive
>     
> 
> For **alert investigation**, the following clusters are checked:
> 
> -   **aoeflight**
> -   **aoelive**
> -   **aoetest**
> -   **arthurlive**
> -   **mythlive**

1.  **For the Test Client Check**, open the folder on your laptop where the Test Client is stored:  
    ![image-2025-7-3_10-46-31.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-3_10-46-31.png)
    
2.  Right-click on the TestClientConfig.json file icon and select Edit with Notepad.
    
3.  Copy the code and replace the entire content of the file based on the cluster:
    
    > **NOTE!**
    > 
    > Blank spaces and indentations are important.
    
    #### Test Client configuration
    

-   **mythlive:**

```json
{
  "titleID": 5,
  "name": "elink",
  "majorVersion": "4.0.0",
  "minorVersion": 0,
  "simPeriodSeconds": 0.125,
  "defaultServer": "aoe"
}

```

**aoeflight, aoelive, aoetest, and arthurlive:**

```json
{
  "titleID": 2,
  "name": "rlink",
  "majorVersion": "4.0.0",
  "minorVersion": 0,
  "simPeriodSeconds": 0.125,
  "defaultServer": "aoe"
}

```

4.  Save the changes and close the file.
    
5.  In the directory path fill in command powershell  
    ![image-2025-7-10_11-6-40.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-10_11-6-40.png)
    
6.  Press the **Enter** button.
    
7.  In the displayed menu in the command prompt, enter the command for the appropriate cluster:
    
    | Cluster | Command | | --- | --- | | aoeflight | .\TestClient_Win.exe -server aoeflight.worldsedgelink.com | | aoelive | .\TestClient_Win.exe -server aoe-api.worldsedgelink.com | | aoetest | .\TestClient_Win.exe -server aoetest.worldsedgelink.com | | arthurlive | .\TestClient_Win.exe -server arthurlive.worldsedgelink.com | | mythlive | .\TestClient_Win.exe -server mythlive.worldsedgelink.com |
    
    ![image-2025-7-8_10-59-53.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_10-59-53.png)
    
8.  Press the **Enter** button.
    
9.  Once the home page is displayed, click the **Profile** tab.
    
    > **IMPORTANT!**
    > 
    > The test client check is an important indicator. If it does not work correctly, it might indicate a critical issue. Immediately create a new incident as described in article [[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation), escalate it as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) and complete investigation steps afterwards.
    
10.  Click the **Platform Login** button:  
    ![image-2024-1-16_8-51-28.png](https://app.glean.com/chat/sanity_check_assets/image-2024-1-16_8-51-28.png)
    
11.  Fill in the **Username** and** Password** with appropriate credentials depending on the cluster stored in [1Password](https://epam.1password.com/).
    
12.  Click the **Login** button:  
    ![image-2025-7-3_12-27-18.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-3_12-27-18.png)
    
13.  Wait for the authentication to complete and act accordingly:
    
    -   **During daily check:**
        -   **if authentication takes 30 seconds or less**, record this information for the report (_Login < 30 sec_) and proceed to step 14.
            
        -   **if authentication takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the provided instructions. Meanwhile, record this information for the report (_Login XX sec_) and proceed to step 14.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The authentication during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if authentication takes more than 3 minutes or fails**, record this information for the report (_Login >3 min_) and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 14.
            
            > **NOTE!**
            > 
            > Monitor the right-hand side Status panel. Actions are queued and removed as they are carried out.
            > 
            > If there is no activity on this panel for 3 minutes, a ticket should be raised with Sev1.
            
    -   **During the alert investigation:** record this information for the report (_Login XX_) and proceed to step 14.
14.  Check the server in the status panel on the right to ensure you are logged into the correct server:  
    ![image-2025-7-3_12-31-58.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-3_12-31-58.png)
    
15.  Click the **Play** tab:  
    ![image-2025-7-7_18-29-52.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-7_18-29-52.png)
    
16.  Click the **Host** tab:  
    ![image-2025-7-7_18-32-3.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-7_18-32-3.png)
    
17.  Click **OK**:  
    ![image-2025-7-7_18-33-56.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-7_18-33-56.png)
    
18.  Wait for the connection to Lobby game to be established and act accordingly:
    
    -   **During daily check:**
        -   **if connection to Lobby game takes up to 30 sec**, record this information for the report (_Battle Servers - Host Game < 30 sec_) and proceed to step 19.
            
        -   **if connection to Lobby game takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the instructions. Meanwhile, record this information for the report (_Battle Servers - Host Game XX_) and proceed to step 19.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The connection to Lobby game during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if connection to Lobby game takes more than 3 minutes or fails**, record this information for the report (_Battle Servers - Host Game >3 min_) and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 19.
            
            > **NOTE!**
            > 
            > Monitor the right-hand side **Status** panel. Actions are queued and removed as they are carried out.
            > 
            > If there is no activity on this panel for 3 minutes, a ticket should be raised with Sev1
            
    -   **During the alert investigation**, record this information for the report (_Battle Servers - Host Game XX_) proceed to step 19.
19.  On the appeared menu from the Slots drop-down menu, in the first slot select AI:*  
    ![image-2025-7-8_11-45-6.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_11-45-6.png)
    
20.  Click the Ready button:  
    ![image-2025-7-8_11-47-9.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_11-47-9.png)
    
21.  Wait for the new screen to be loaded and act depending on the loading time:
    
    > **NOTE!**
    > 
    > Once the next screen is displayed, the virtual in-game action and test are successful.
    
    ![image-2025-7-8_11-58-11.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_11-58-11.png)
    
    -   **During daily check:**
        
        -   **if the creation of the game takes up to 30 sec**, record this information for the report (_Battle Servers - Load into game < 30 sec_) and proceed to step 22.
            
        -   **if the creation of the game takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) in MS Teams and follow the instructions. Meanwhile, record this information for the report (_Battle Servers - Load into game XX sec_) and proceed to step 22.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The creation of the game during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if the creation of the game takes more than 3 minutes or fails**, record this information for the report (_Battle Servers - Load into game >3 min / failed_) and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 22.
            
    -   **During the alert investigation**, record this information for the report (_Battle Servers - Load into game XX_) and proceed to step 22.
        
22.  On the displayed page, select any button to complete the game:  
    ![image-2025-7-8_12-15-51.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_12-15-51.png)
    
    > **NOTE!**
    > 
    > A disconnecting screen is displayed  
    > ![image-2025-7-8_12-23-34.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_12-23-34.png)
    
23.  Wait for the game completion and act depending on the time it takes:
    
    -   **During daily check:**
        -   **if the game completion takes up to 30 sec**, record this information for the report (_Battle Servers - Completing a game < 30 sec_) and proceed to step 24.
            
        -   **if the game completion takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the provided instructions. Meanwhile, record this information for the report (_Battle Servers - Completing a game XX sec_) proceed to step 24.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The completion of the game during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if the game completion takes more than 3 minutes or fails**, record this information for the report (_Battle Servers - Completing a game >3 min / failed)_ and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 24.
            
            > **NOTE!**
            > 
            > Monitor the right-hand side **Status** panel. Actions are queued and removed as they are carried out.
            > 
            > If there is no activity on this panel for 3 minutes, a ticket should be raised with Sev1
            
    -   **During the alert investigation**, record this information for the report (_Battle Servers - Completing a game XX_) and proceed to step 24.
24.  In the **Party** tab, click the** Create Party** button:  
    ![image-2025-7-8_12-29-44.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_12-29-44.png)
    
25.  Wait for the lobby slots to become active and act depending on the waiting time:  
    ![image-2025-11-28_16-8-54.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-8-54.png)
    
    -   **During daily check:**
        
        -   **if the party creation takes up to 30 sec**, record this information for the report (_Lobby Servers - Create Party < 30 sec_) and proceed to step 26.
            
        -   **if the party creation takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the instructions. Meanwhile, record this information for the report (_Lobby Servers - Create Party XX sec_) and proceed to step 26.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The party creation during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if the party creation takes more than 3 minutes or fails**, record this information for the report (_Lobby Servers - Create Party >3 min / failed_) and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 26.
            
    -   **During the alert investigation:** record this information for the report (_Lobby Servers - Create Party XX_) and proceed to step 26.
        
26.  Click the Leave Party button:  
    ![image-2025-7-8_12-37-43.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_12-37-43.png)
    
27.  Click the **Chat** tab.
    
28.  Select one of the Available Channels.
    
29.  Click the **Join** button:  
    ![chat join.jpg](https://app.glean.com/chat/sanity_check_assets/chat_join.jpg)
    
30.  Check that you successfully join the channel in the **Channel** and* _**Joined sections**:_  
    ![image-2025-7-8_13-2-59.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_13-2-59.png)
    
31.  Write a test message in the text box.
    
32.  Click Send button:  
    ![chat test.jpg](https://app.glean.com/chat/sanity_check_assets/chat_test.jpg)
    
33.  Wait for the message to be displayed in the **Channe** l section (i.e., the test is successful) and act depending on the waiting time:  
    ![image-2025-7-8_13-10-46.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-8_13-10-46.png)
    
    -   **During daily check:**
        -   **if the communication with the Chat takes up to 30 sec**, record this information for the report (_Chat check successful_) and proceed to step 34.
            
        -   **if the communication with the Chat takes more than 30 sec but less than 3 minutes**, post the following message into [EPAM support channel](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) and follow the instructions. Meanwhile, record this information for the report (_Chat check XX_) and proceed to step 34.
            
            > **NOTE!**
            > 
            > @everyone, hi team!  
            > The the communication with the chat during the cluster check for name of the cluster takes approximately ** seconds.  
            > Please advise if any actions are needed from the L1 team?
            
        -   **if the communication with the Chat takes more than 3 minutes or fails**, record this information for the report (_Chat check >3 min / failed_) and [Sev2 Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 34.
            
            > **NOTE!**
            > 
            > Monitor the right-hand side **Status** panel. Actions are queued and removed as they are carried out.
            > 
            > If there is no activity on this panel for 3 minutes, a ticket should be raised with Sev1.
            
    -   **During the alert investigation**, record this information for the report (_Chat check XX_) and proceed with [Cluster Check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#cluster-check).
34.  Once the checks for test client are complete, proceed to the next check.
    

### Leader Board Check

1.  **For Leader Board Check**, go to [AoE Live Leaderboard](https://aoe-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty).
    
2.  Check the result **message** and act accordingly:
    
    -   **if there is a part of code with SUCCESS status,** record this information for the report and proceed to step 3.
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to step 3.  
        ![image-2025-11-28_16-16-2.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-16-2.png)
3.  Go to [Myth Live Leaderboard](https://athens-live-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=athens&format=jsonpretty).
    
4.  Check the result **message** and act accordingly:
    
    -   **if there is a part of code with SUCCESS status,** record this information for the report and proceed to step 5.
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the Checks are finished. Then proceed to step 5.  
        ![image-2025-11-28_16-16-41.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-16-41.png)
5.  Go to [AoE Flighting Leaderboard](https://flighting-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty).
    
6.  Check the result **message** and act accordingly:
    
    -   **if there is a part of code with SUCCESS status,** record this information for the report and proceed to step 9.
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to step 9.  
        ![image-2025-11-28_16-17-19.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-17-19.png)
7.  Go to [AoE Test Leaderboard](https://aoetest-api.worldsedgelink.com/community/Leaderboard/getLeaderboard2?leaderboard_id=1&sortBy=1&start=1&count=200&title=age2&format=jsonpretty).
    
8.  Check the result **message** and act accordingly:
    
    -   **if there is a part of code with SUCCESS status,** proceed to [Azure Service Health check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#azure-service-health-check).
    -   **if there is a part of code with another status,** record this information for [new Incident creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished. Then proceed to [Azure Service Health check](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#azure-service-health-check).  
        ![image-2025-11-28_16-17-58.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-17-58.png)

### Azure Service Health

1.  **For Azure Service Health** check go to [Azure Service Health](https://portal.azure.com/#view/Microsoft_Azure_Health/AzureHealthBrowseBlade/~/serviceIssues) page
    
2.  Check the affected Locations (red location status) and act accordingly:
    
    -   **No affected locations:**  
        ![azure cluster check.png](https://app.glean.com/chat/sanity_check_assets/azure_cluster_check.png)
        
        **Affected locations detected:**  
        ![image-2025-11-27_17-18-5.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-27_17-18-5.png)
        
    -   **if there are NO Affected locations** proceed to [processing cluster check results](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#processing-cluster-check-results).
        
    -   **if there are Affected locations,** make a screenshot of the dashboard and save it locally to be later uploaded and proceed to step 3.
        
3.  Click on the **Issue name** link:  
    ![image-2025-11-27_17-17-16.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-27_17-17-16.png)
    
4.  Make a screenshot of the page and save it locally to be later uploaded into the related ADO ticket.
    
5.  Copy the **issue name** and use it for naming when creating a [new Incident](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) after all the checks are finished:  
    ![image-2025-11-28_16-14-36.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-14-36.png)
    
6.  Proceed to [processing cluster check results](https://app.glean.com/chat/aec01822b73241c6af4f88ef56797bf6?qe=https%3A%2F%2Fepam-prod-be.glean.com#processing-cluster-check-results) → tab _**Issues detected.**_
    

## 2. Processing cluster check results

### Daily Cluster Sanity Check results

Depending on the Daily Cluster Sanity Check results, proceed with the following steps:

**If no issues were found during the Daily Cluster Sanity Check**, send the following report using** mail template**: [XBOX-AOE_Daily_Cluster_Sanity_Check_Report.msg](https://kb.epam.com/download/attachments/2245597630/XBOX-AOE_Daily_Cluster_Sanity_Check_Report.msg?version=2&modificationDate=1789027944742&api=v2)

#### No-issues email report template

Field

Value

**FROM**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**TO**

<[edge_link@microsoft.com](mailto:edge_link@microsoft.com)>;

**CC**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**Subject**

XBOX-AOE: Daily Cluster Sanity Check 1:00 AM/PM

**Message**

Hello Team, We have performed our Sanity Check for the following Clusters: - aoelive - arthurlive - mythlive**Test Plan AoeLive Cluster Check.** - Login < 30 sec - Lobby Servers - Create Party < 30 sec - Battle Servers - Host Game < 30 sec - Battle Servers - Load into game < 30 sec - Battle Servers - Completing a game < 30 sec - Chat check successful**Test Plan Arthurlive Cluster Check.** - Login < 30 sec - Lobby Servers - Create Party < 30 sec - Battle Servers - Host Game < 30 sec - Battle Servers - Load into game < 30 sec - Battle Servers - Completing a game < 30 sec - Chat check successful**Test Plan Mythlive Cluster Check.** - Login < 30 sec - Lobby Servers - Create Party < 30 sec - Battle Servers - Host Game < 30 sec - Battle Servers - Load into game < 30 sec - Battle Servers - Completing a game < 30 sec - Chat check successfulLeader Board Test Were Successful / FailedAzure Service HealthAttach screenshot from Service Health Best regards, Epam signature

![image-2025-11-28_16-20-10.png](https://app.glean.com/chat/sanity_check_assets/image-2025-11-28_16-20-10.png)

1.  **If any issues were found during the Daily Cluster Sanity Check,** make sure that an ADO ticket is created as described in article [[L1] ADO Ticket Creation](https://kb.epam.com/spaces/XBOXAOE/pages/2579410428/L1+ADO+Ticket+Creation) (→ tab***[Ticket for Cluster Check](https://kb.epam.com/display/XBOXAOE/%5BL1%5D+ADO+Ticket+Creation#TicketforClusterCheck)***).
    
    To register an **ADO ticket from an e-mail alert (Azure or PagerDuty)** perform the following steps:
    
    1.  Login to the [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/create/Issue?templateId=4a21c7a6-bafa-4ea2-bc95-e73bb1f2b785&ownerId=64c79b63-a125-4317-a06f-a60763622252) Issue creation page using your EPAM credentials.
        
    2.  In the **Enter Title** section type in _**test.**_
        
    3.  Click the **Save** button:![image-2025-6-23_13-35-2.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-23_13-35-2.png)
        
    4.  Once the ADO ticket has been created, copy the **ADO ticket number** for future reference:  
        ![image-2025-6-30_10-54-53.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_10-54-53.png)
        
    5.  Proceed to sending the status update notification as described in the related instruction depending on the initial alert type:
        
        -   **for a Fired Azure alert:** see [[L1] Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2607572290/L1+Azure+Alerts+handling) → tab [Send a status update notification](https://kb.epam.com/display/XBOXAOE/%5BL1%5D+Fired+Azure+Alerts+handling#id-%5BL1%5DFiredAzureAlertshandling-SendstatusupdatenotificationinPagerDutySendastatusupdatenotificationsection)
        -   **for a PagerDuty alert**: see [[L1] Fired Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2697079781/L1+Fired+Azure+Alerts+handling)
    
    To register a **new ADO ticket from an Azure Scheduled Maintenance** notification, perform the following steps:
    
    1.  Log in to the [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/create/Issue?templateId=4a21c7a6-bafa-4ea2-bc95-e73bb1f2b785&ownerId=64c79b63-a125-4317-a06f-a60763622252) Issue creation page using your EPAM credentials.
        
    2.  Fill in the following fields based on the issue type:
        
        | Field | Value | | --- | --- | | Enter Title | [EdgeLink] [INFORMATIONAL] [ Cluster ] - Azure Scheduled Maintenance Example: [EdgeLink] [INFORMATIONAL] [AOEFLIGHT] - Azure Scheduled Maintenance | | Assignee | Your First Name Last Name | | Add Tag (Label) | EPAMNOC + aoelive / aoeflight / aoetest / arthurlive / mythlive + EPAML1.5 + Maintenance | | Area | WELink\EPAM NOC | | Description | Mail body with the header starting from the From: field | | Game | All | | Priority | 3 | | Attachments / Comments | Add the Azure Notification when the Maintenance is "In Progress" and has "Completed" Add all Azure Alerts triggered during the timeframe of the Maintenance related to the Cluster |
        
        3. Click the Save button:  
        ![image-2025-6-30_12-7-24.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_12-7-24.png)
        
        4.  Change the issue state to Active:  
            ![image-2025-7-21_15-41-57.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-21_15-41-57.png)
        
        5. Click **Save** again.
        
        6.  Once the ADO ticket has been created, proceed to the next steps described in article [[L1] Azure Scheduled Maintenance / Outage notifications handling](https://kb.epam.com/spaces/XBOXAOE/pages/2392306670/L1+Azure+Scheduled+Maintenance+Outage+notifications+handling) → _step 3_.
        
        | Field | Value | | --- | --- | | Enter Title | [EdgeLink] [CRITICAL] [ Cluster ] - CCU Impact Example: [EdgeLink] [CRITICAL] [AOELIVE] - CCU Impact | | Assignee | Your First Name Last Name | | Add Tag (Label) | EPAMNOC + aoelive / arthurlive / mythlive | | Area | WELink\EPAM NOC | | Description | Screenshot of CCU Impact | | Game | All | | Priority | 1 | | Attachments / Comments | n/a |
        
        3. Click the Save button:  
        ![image-2025-6-30_12-7-24.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_12-7-24.png)
        
        4.  Change the issue state to Active:  
            ![image-2025-7-21_15-41-57.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-21_15-41-57.png)
        
        5. Click **Save** again.
        
        6.  Once the ADO ticket has been created, proceed to the [[L1] Azure Scheduled Maintenance / Outage notifications handling](https://kb.epam.com/spaces/XBOXAOE/pages/2392306670/L1+Azure+Scheduled+Maintenance+Outage+notifications+handling) → step 6.
    
    To register **a new ADO ticket identified during Cluster Check**, perform the following steps:
    
    1.  Log in to the [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/create/Issue?templateId=4a21c7a6-bafa-4ea2-bc95-e73bb1f2b785&ownerId=64c79b63-a125-4317-a06f-a60763622252) Issue creation page using your EPAM credentials.
        
    2.  Fill in the following fields based on the issue type and severity:
        
        | Field | Value for issues with CCU impact | | --- | --- | | Enter Title | [EdgeLink] [CRITICAL] [ CLUSTER ] - CC - Description of the issue Example: [EdgeLink] [CRITICAL] [AOELIVE] - CC - Total CCU on cluster - gaps on the metric | | Assignee | Your First Name Last Name | | Add Tag (Label) | EPAMNOC + Cluster Check + aoelive / arthurlive / mythlive | | Area | WELink\EPAM NOC | | Description | Add the screenshot of the identified issue | | Game | All | | Priority | 1 | | Attachments / Comments | Add screenshots of the Cluster Check investigation as comments in the ADO ticket |
        
        | Field | Value for issues without CCU impact | | --- | --- | | Enter Title | [EdgeLink] [WARNING] [ CLUSTER ] - CC - Description of the issue Example: [EdgeLink] [ WARNING ] [AOELIVE] - CC - Too many 4xx errors per 5 minute interval | | Assignee | Your First Name Last Name | | Add Tag (Label) | EPAMNOC + Cluster Check + aoelive / arthurlive / mythlive | | Area | WELink\EPAM NOC | | Description | Add the screenshot of the identified issue | | Game | All | | Priority | 2 | | Attachments / Comments | Add screenshots of the Cluster Check investigation as comments in the ADO ticket |
        
        ![image-2025-6-25_18-46-17.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-25_18-46-17.png)
        
    3.  Click the Save button:  
        ![image-2025-6-30_12-7-24.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_12-7-24.png)
        
    4.  Once the ADO ticket has been created, proceed to [[L1] Daily Cluster Sanity Check → Processing cluster check results](https://kb.epam.com/spaces/XBOXAOE/pages/2702409893/L1+Daily+Cluster+Sanity+Check#id-%5BL1%5DDailyClusterSanityCheck-2.Processingclustercheckresults)
        
    
    To register **a new ADO ticket reported during the phone call**, perform the following steps:
    
    1.  Log in to the [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/create/Issue?templateId=4a21c7a6-bafa-4ea2-bc95-e73bb1f2b785&ownerId=64c79b63-a125-4317-a06f-a60763622252) Issue creation page using your EPAM credentials.
        
    2.  Fill in the fields as follows:
        
        | Field | Value | | --- | --- | | Enter Title | [EdgeLink] [ CRITICAL / WARNING / INFORMATIONAL ] [ CLUSTER ] - Issue short description Example: [EdgeLink] [INFORMATIONAL] [aoelive] - App Gateway - Excessive Rate Limiting | | Assignee | Your Name Surname | | Add Tag (Label) | EPAMNOC + aoelive / aoeflight / arthurlive / mythlive / elf telemetry | | Area | WELink\EPAM NOC | | Description | Caller's First Name/Last Name : Name Surname Contacts : e-mail phone number (in international format) Priority of the Incident : P1 / P2 / P3 Issue description: errors how long the problem lasts how many people/teams are affected | | Game | All | | Priority | Select an appropriate one depending on the information provided by the user: 1/ 2 / 3 |
        
    3.  Click the Save button:  
        ![image-2025-6-30_12-7-24.png](https://app.glean.com/chat/sanity_check_assets/image-2025-6-30_12-7-24.png)
        
    4.  Once the ADO ticket has been created, proceed to further steps described in article [[L1] Phone Calls Handling](https://kb.epam.com/spaces/XBOXAOE/pages/2040709728/L1+Phone+Calls+Handling) → tab _Real Person_.
        
2.  Whenever a ticket is created, add a justification in the **Comments** section of the ADO ticket explaining why the ticket is being created:
    
    > **NOTE!**
    > 
    > ISSUE XXXXXX - ticket will be escalated to the L2 team.
    
    > **NOTE!**
    > 
    > Every created ticket must contain a justification comment. The comment must clearly state the identified issue and the planned action.
    > 
    > Tickets without a comment or a justified investigation are considered incomplete.
    
3.  Post a message from **Microsoft (Guest)** account in MS Teams in the **[Edgelink > EPAM support](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47)** channel:
    
    > **NOTE!**
    > 
    > ISSUE XXXXXX - TITLE - PRIORITY - @EPAM support
    
4.  Once the ADO Ticket has been created, select the relevant recipient from the table below:
    
    | Conditions (cluster, issue type) | Send the email to ( pagerduty email) / ticket creation | | --- | --- | | aoeflight | [R022NNFK5EXO5TQODE21R8PUS0ABGZMM@edgelink.pagerduty.com](mailto:R022NNFK5EXO5TQODE21R8PUS0ABGZMM@edgelink.pagerduty.com) | | aoelive | [R02IINFF2RJH6XHCPZMXIPUYV0XZEN2V@edgelink.pagerduty.com](mailto:R02IINFF2RJH6XHCPZMXIPUYV0XZEN2V@edgelink.pagerduty.com) | | Azure Service Health issue | | | aoetest | [R028KECLXYLL5UZSWBTXLTWQG07783CJ@edgelink.pagerduty.com](mailto:R028KECLXYLL5UZSWBTXLTWQG07783CJ@edgelink.pagerduty.com) | | arthurlive | [R02BWPNQGNYFBO0MALPMMA0U51KJVIDG@edgelink.pagerduty.com](mailto:R02BWPNQGNYFBO0MALPMMA0U51KJVIDG@edgelink.pagerduty.com) | | mythlive | [R020KFXNB1QKD9286P8MG2SDM197879E@edgelink.pagerduty.com](mailto:R020KFXNB1QKD9286P8MG2SDM197879E@edgelink.pagerduty.com) | | tournament | [R02J04J8Q71OK3Z79D6LLDTNG03T40S8@edgelink.pagerduty.com](mailto:R02J04J8Q71OK3Z79D6LLDTNG03T40S8@edgelink.pagerduty.com) |
    
5.  Send the following email to create an incident inside PagerDuty using **mail template**: [XBOX-AOE_FiredSev12Azure_Monitor_Alertcluster_Issue_Identified.msg](https://kb.epam.com/download/attachments/2245597630/XBOX-AOE_FiredSev12Azure_Monitor_Alertcluster_Issue_Identified.msg?version=2&modificationDate=1786434752304&api=v2)
    
    #### PagerDuty incident notification template
    

Field

Value

**FROM**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**TO**

<[edge_link@microsoft.com](mailto:edge_link@microsoft.com)>; Pagerduty email

**CC**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**Subject**

Fired:Sev1/2/3 Azure Monitor Alert cluster - Issue Identified during Cluster Check

**Message**

An issue was identified on Cluster xxxx on Board xxxx. The following ticket was created xxxx. Attach Screenshot of the issue(s) identified EPAM SIGNATURE

6.  Ensure that the notification for the PagerDuty alert is triggered within 10 minutes:
    
    -   **if the PagerDuty incident is created automatically,** process the new PagerDuty Incident as described in article [[L1] Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2607572290/L1+Azure+Alerts+handling).
        
    -   **if the PagerDuty incident is NOT created automatically,** manually create a new PagerDuty incident as described in article [[L1] PagerDuty ticket creation](https://kb.epam.com/spaces/XBOXAOE/pages/2581370814/L1+PagerDuty+ticket+creation). Then process the new PagerDuty Incident as described in article [[L1] Azure Alerts handling](https://kb.epam.com/spaces/XBOXAOE/pages/2607572290/L1+Azure+Alerts+handling).
        
7.  **FOR EU-IN Cluster Checks:** Act depending on the ticket Severity:
    
    -   **if a Sev1 Ticket is created (ADO & PD)**, immediately start [MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process)
        
    -   **if a Sev2 Ticket is created (ADO & PD),** add it in your_**Cluster Check email**_ and leave the tickets pending in HO to be escalated during BH - [Daily end-of-shift Report](https://kb.epam.com/spaces/XBOXAOE/pages/2327981263/L1+Daily+end-of-shift+Report).
        
8.  Send the following repot using **mail template**: [XBOX-AOE_Daily_Cluster_Sanity_Check_Report_issue_detected.msg](https://kb.epam.com/download/attachments/2245597630/XBOX-AOE_Daily_Cluster_Sanity_Check_Report_issue_detected.msg?version=2&modificationDate=1789028141284&api=v2)
    

#### Issue-found daily report template

Field

Value

**FROM**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**TO**

<[edge_link@microsoft.com](mailto:edge_link@microsoft.com)>;

**CC**

<[supportxbox-aoel1@epam.com](mailto:supportxbox-aoel1@epam.com)>

**Subject**

XBOX-AOE: Daily Cluster Sanity Check 1:00 AM/PM

**Message**

Hello Team, We have performed our Sanity Check for the following Clusters: - aoelive - arthurlive - mythlive An issue was identified on Cluster xxxx on Board xxxx. The following ticket was created xxxx. Attach Screenshot of the issue(s) identified**Test Plan AoeLive Cluster Check.** - Login < 30 sec / XX sec / >3 min / failed - Lobby Servers - Create Party < 30 sec / XX sec / >3 min / failed - Battle Servers - Host Game < 30 sec / XX sec / >3 min / failed - Battle Servers - Load into game < 30 sec / XX sec / >3 min / failed - Battle Servers - Completing a game < 30 sec / XX sec / >3 min / failed - Chat check successful / XX sec / >3 min / failed**Test Plan Arthurlive Cluster Check.** - Login < 30 sec / XX sec / >3 min / failed - Lobby Servers - Create Party < 30 sec / XX sec / >3 min / failed - Battle Servers - Host Game < 30 sec / XX sec / >3 min / failed - Battle Servers - Load into game < 30 sec / XX sec / >3 min / failed - Battle Servers - Completing a game < 30 sec / XX sec / >3 min / failed - Chat check successful / XX sec / >3 min / failed**Test Plan Mythlive Cluster Check.** - Login < 30 sec / XX sec / >3 min / failed - Lobby Servers - Create Party < 30 sec / XX sec / >3 min / failed - Battle Servers - Host Game < 30 sec / XX sec / >3 min / failed - Battle Servers - Load into game < 30 sec / XX sec / >3 min / failed - Battle Servers - Completing a game < 30 sec / XX sec / >3 min / failed - Chat check successful / XX sec / >3 min / failedLeader Board Test Were Successful / FailedAzure Service Health Attach screenshot from Service Health Best regards, Epam signature

### Alert investigation

1.  Within Alert investigation result processing depending on the Test Client Check results post the following comment in the ADO ticket:

```
> **NOTE!**

```

```
>
> **Test Plan AoeFlight /  AoeLive / AoeTest / Arthurlive / MythLive Cluster Check.**
>
> - Login \< 30 sec / XX sec / \>3 min / failed
> - Lobby Servers - Create Party  \< 30 sec / XX sec / \>3 min / failed
> - Battle Servers - Host Game  \< 30 sec / XX sec / \>3 min / failed
> - Battle Servers - Load into game \< 30 sec / XX sec / \>3 min / failed
> - Battle Servers - Completing a game \< 30 sec / XX sec / \>3 min / failed
> - Chat check successful / failed

```

2. Make sure that all the necessary screenshots from other checks are attached to the ADO ticket.

3.  Process the ticket further depending on the alert severity, affected service and time:
    
    #### Sev1
    

-   **Alert type / affected service:** Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   **Alert type / affected service:** CCU Impact; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** in more than 10 minutes; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   Alert type / affected service: NO CCU Impact AND NO Test Client Error; Auto-resolved: within 10 minutes; Alert delivery time: BH: - Mon - Fri, 10 AM - 5:59 PM CST / CDT*; Required Actions: 1. Downgrade the ADO ticket to Sev2. 2. Update the ADO ticket title by changing [CRITICAL] tag to [Auto-Resolved]. 3. Process the ticket as described in article [[L1] BH Tickets Escalation](https://kb.epam.com/spaces/XBOXAOE/pages/2592348172/L1+BH+Tickets+Escalation)
-   Alert type / affected service: NO CCU Impact AND NO Test Client Error; Auto-resolved: within 10 minutes; Alert delivery time: OOBH: - Mon - Fri, 6 PM - 09:59 AM CST / CDT* - Weekends; Required Actions: 1. Downgrade the ADO ticket to Sev2. 2. Update the ADO ticket title by changing [CRITICAL] tag to [Auto-Resolved]. 3. Add the information about the alert to the HO report to the next agent so that it could be actioned on the next Business Day (Mon - Fri, 10 AM - 5:59 PM CST / CDT*) as described in article [[L1] Daily end-of-shift Report](https://kb.epam.com/spaces/XBOXAOE/pages/2327981263/L1+Daily+end-of-shift+Report)

#### Sev2

-   **Alert type / affected service:** Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
    
-   **Alert type / affected service:** CCU Impact; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
    
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** BH: - Mon - Fri, 10 AM - 5:59 PM CST / CDT*; **Required Actions:** Process the ticket as described in article [[L1] BH Tickets Escalation](https://kb.epam.com/spaces/XBOXAOE/pages/2592348172/L1+BH+Tickets+Escalation)
    
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** OOBH: - Mon - Fri, 6 PM - 09:59 AM CST / CDT* - Weekends; **Required Actions:** Add the information about the alert to the HO report to the next agent so that it could be actioned on the next Business Day (Mon - Fri, 10 AM - 5:59 PM CST / CDT*) as described in article [[L1] Daily end-of-shift Report](https://kb.epam.com/spaces/XBOXAOE/pages/2327981263/L1+Daily+end-of-shift+Report)
    
    > **NOTE!**
    > 
    > * To define the time in your location, follow the link to the [time converter](https://www.worldtimebuddy.com/?pl=1&lid=0,212,312,206,213,313,212,305,205,314&h=212&hf=0)
    
    #### Ticket closure procedure
    

**Alert Severity:**

Any

**Alert type / affected service:**

Any

**Alert delivery time:**

Any

**Required Actions:**

1.  Close the ADO ticket as described in article [[L1] ADO Ticket Closure](https://kb.epam.com/spaces/XBOXAOE/pages/2594259516/L1+ADO+Ticket+Closure).
    
    > **IMPORTANT!**
    > 
    > When a ticket is resolved, **it should be closed in both systems [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/recentlyupdated/) AND [PagerDuty](https://edgelink.pagerduty.com/incidents).**
    
    To close a ticket in [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/recentlyupdated/) perform the following steps:
    
    1.  Open the ticket in [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/recentlyupdated/).
        
    2.  Double-check that the investigation steps are documented in the ticket.
        
    3.  Change the **State** of the ticket to** Closed:**  
        ![image-2025-7-15_13-44-33.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_13-44-33.png)
        
    4.  Post the final resolution comment:
        
        > **NOTE!**
        > 
        > Alert auto-resolved in 10 minutes or less with no impact on CCU or Test Client Errors
        
    5.  Add a note in the **Comments** section providing a justification on why the ticket has been closed.
        
        _Examples:_
        
        -   _Ticket closed as per L2/L3 instruction._
        -   _Closing ticket and merging PagerDuty Incident to PD XXXX._
        
        > **NOTE!**
        > 
        > A ticket must never be closed without a closure justification in the **Comments** section.
        
        ![image-2025-7-15_12-23-22.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_12-23-22.png)
        
    6.  Act based on the ticket severity:
        
        -   if the ticket has Sev1, change [Critical] in the subject to [Auto-Resolved]. Then proceed with step 6.  
            ![image-2025-7-15_12-31-27.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_12-31-27.png)
        -   **Downgrade Priority from P1 to P2.**
        -   **if the ticket has Sev2 or Sev3,** proceed with step 6.
    7.  Add the Tag (Label): EPAML1.5  
        ![image-2025-7-15_12-37-34.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_12-37-34.png)
        
    8.  Follow the Pager Duty ticket closure procedure as described in article [[L1] PagerDuty ticket closure](https://kb.epam.com/spaces/XBOXAOE/pages/2607572565/L1+PagerDuty+ticket+closure).
        
2.  Close the PagerDuty Incident as described in article [[L1] PagerDuty ticket closure](https://kb.epam.com/spaces/XBOXAOE/pages/2607572565/L1+PagerDuty+ticket+closure).
    
    > **IMPORTANT!**
    > 
    > When a ticket is resolved, **it should be closed in both systems [Azure ADO](https://dev.azure.com/Worlds-Edge/WELink/_workitems/recentlyupdated/) AND [PagerDuty](https://edgelink.pagerduty.com/incidents).**
    > 
    > **Ensure that the ticket is closed in ADO** as described in article [[L1] ADO Ticket Closure](https://kb.epam.com/spaces/XBOXAOE/pages/2594259516/L1+ADO+Ticket+Closure) before proceeding with the below steps.
    
    To close a ticket in [Pager Duty](https://edgelink.pagerduty.com/incidents) perform the following steps:
    
    1.  Open the related ticket in [Pager Duty](https://edgelink.pagerduty.com/incidents)
        
    2.  Act depending on the ADO ticket severity:
        
        -   if the ADO ticket has Sev1, click Priority button and update the Priority to Auto. Then proceed with step 3.  
            ![image-2024-3-26_13-17-6.png](https://app.glean.com/chat/sanity_check_assets/image-2024-3-26_13-17-6.png)
            
        -   if the ticket has Sev2 or Sev3, proceed with step 3.
            
    3.  Click the **Resolve** button:  
        ![image-2024-3-26_13-35-13.png](https://app.glean.com/chat/sanity_check_assets/image-2024-3-26_13-35-13.png)
        
    4.  Remove the text from the **Resolution Note** section if there is any.
        
    5.  Post the message in the **Resolution Note** section depending on the closure reason:
        
        -   if the Incident is auto-resolved within 10 minutes:
        
        > **NOTE!**
        > 
        > The incident ADO ticket title has been resolved. Alert auto-resolved in 10 minutes or less with no impact on CCU or Test Client Errors
        
        6. Press the **Resolve Incident** button:  
        ![XBOX_PagerDuty_close1.png](https://app.glean.com/chat/sanity_check_assets/XBOX_PagerDuty_close1.png)
        
        7.  Click the Send Status Update button:  
            ![image-2024-10-22_10-37-43.png](https://app.glean.com/chat/sanity_check_assets/image-2024-10-22_10-37-43.png)
            
        8.  In the **Select a communication template** drop-down, select the option based on the ticket severity:
            
        
        -   if the ticket has Sev1 select the Auto Resolved Template.
        -   **if the ticket has****Sev2** select the** Final Closure Template.**
        -   if the ticket has Sev3 select the Sev3 Closure Template.
        
        9.  Click the Preview button:  
            ![image-2025-7-15_16-39-57.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_16-39-57.png)
            
        10.  Click the **Edit Email** button to update the email body:  
            ![image-2025-7-17_16-55-57.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-17_16-55-57.png)
            
        
        11. In the Select CCU/Services Impacted? line leave the NO option:  
        ![image-2025-7-15_17-3-18.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_17-3-18.png)
        
        12.  Add the created **ADO Ticket number** into the link string:  
            ![image-2025-7-15_17-5-21.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_17-5-21.png)
            
        13.  Make sure that the updated link is clickable.
            
        14.  Click the **Send Update** button:  
            ![image-2025-7-15_17-14-8.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_17-14-8.png)
            
        15.  Post the following notification from the Microsoft (Guest) account in MS Teams, in the **[EPAM support](https://teams.microsoft.com/l/channel/19%3Adafce2499dd54f198259659ecca8e7ad%40thread.tacv2/EPAM%20support?groupId=e4f886a6-1b0d-472b-92e2-bb8f8a893db5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47)** channel, as a reply to the original post that was made when the ticket was created:
            
        
        > **NOTE!**
        > 
        > Alert auto-resolved, no CCU impact detected. Ticket closed.
        
        ![image-2025-7-15_17-12-44.png](https://app.glean.com/chat/sanity_check_assets/image-2025-7-15_17-12-44.png)
        
        -   **if the Incident is triggered during the planned cluster maintenance / outage:**
        
        > **NOTE!**
        > 
        > Closing PagerDuty Incident received during the Maintenance Window.
        
        6. Press the **Resolve Incident** button:
        
        ![XBOX_PagerDuty_close.png](https://app.glean.com/chat/sanity_check_assets/XBOX_PagerDuty_close.png)
        
    
    #### Alert investigation: ticket handling matrix
    

#### Sev1

-   **Alert type / affected service:** Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   **Alert type / affected service:** CCU Impact; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** in more than 10 minutes; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
-   Alert type / affected service: NO CCU Impact AND NO Test Client Error; Auto-resolved: within 10 minutes; Alert delivery time: BH: - Mon - Fri, 10 AM - 5:59 PM CST / CDT*; Required Actions: 1. Downgrade the ADO ticket to Sev2. 2. Update the ADO ticket title by changing [CRITICAL] tag to [Auto-Resolved]. 3. Process the ticket as described in article [[L1] BH Tickets Escalation](https://kb.epam.com/spaces/XBOXAOE/pages/2592348172/L1+BH+Tickets+Escalation)
-   Alert type / affected service: NO CCU Impact AND NO Test Client Error; Auto-resolved: within 10 minutes; Alert delivery time: OOBH: - Mon - Fri, 6 PM - 09:59 AM CST / CDT* - Weekends; Required Actions: 1. Downgrade the ADO ticket to Sev2. 2. Update the ADO ticket title by changing [CRITICAL] tag to [Auto-Resolved]. 3. Add the information about the alert to the HO report to the next agent so that it could be actioned on the next Business Day (Mon - Fri, 9 PM CST / CDT*) as described in article [[L1] Daily end-of-shift Report](https://kb.epam.com/spaces/XBOXAOE/pages/2327981263/L1+Daily+end-of-shift+Report)

#### Sev2

-   **Alert type / affected service:** Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
    
-   **Alert type / affected service:** CCU Impact; **Auto-resolved:** N/A; **Alert delivery time:** N/A; **Required Actions:** 1. Immediately escalate the incident as described in article [[L1] Major Incident and MIM Process](https://kb.epam.com/spaces/XBOXAOE/pages/2274862346/L1+Major+Incident+and+MIM+Process) 2. Complete the investigation steps afterward.
    
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** BH: - Mon - Fri, 10 AM - 5:59 PM CST / CDT*; **Required Actions:** Process the ticket as described in article [[L1] BH Tickets Escalation](https://kb.epam.com/spaces/XBOXAOE/pages/2592348172/L1+BH+Tickets+Escalation)
    
-   **Alert type / affected service:** NO CCU Impact AND NO Test Client Error; **Auto-resolved:** N/A; **Alert delivery time:** OOBH: - Mon - Fri, 6 PM - 09:59 AM CST / CDT* - Weekends; **Required Actions:** Add the information about the alert to the HO report to the next agent so that it could be actioned on the next Business Day (Mon - Fri, 9 PM CST / CDT*) as described in article [[L1] Daily end-of-shift Report](https://kb.epam.com/spaces/XBOXAOE/pages/2327981263/L1+Daily+end-of-shift+Report)
    
    > **NOTE!**
    > 
    > * To define the time in your location, follow the link to the [time converter](https://www.worldtimebuddy.com/?pl=1&lid=0,212,312,206,213,313,212,305,205,314&h=212&hf=0)
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5OTc3MDkzMjZdfQ==
-->