---
lab:
    title: 'Lab 02: Configure your environment for Teams Voice Usage'
    type: 'Answer Key'
    module: 'Module 01: Plan and configure Teams Phone'
---

# Lab 02: Configure your environment for Teams Phone
# Student lab answer key

## Lab scenario

Contoso want to setup Teams Phone for their users. 

Firstly, our administrator wants to ensure the network is capable of running Microsoft teams, we will do this by completing the following tasks:

- Evaluate our network bandwidth with Network Planner

- Test our network performance with the Teams Network Assessment

Next, we need to configure our tenant ready for acquiring phone numbers and assigning them to users, before we can acquire and assign phone numbers we need to configure out network topology and emergency calling addresses

- Configure a basic network topology and emergency calling addresses

Voice Policies allow us to configure specific parts of Teams Phone. We have a requirement for extension dialing and call park and some of our users do not want their number presented when making outbound calls. Finally, there is a number we wish to block from making inbound calls to Contoso. 

- Configure Voice policies to meet Contoso requirements

Now we will acquire and assign phone numbers to a user and perform a test call and configure audio conferencing for our users

- Assign licenses and phone numbers to a user for calling

- Configure audio conferencing

Finally we will configure Call Queues and Auto Attendants for inbound calls to Contoso

- Configure Call Queues and Auto Attendants 

## Lab Setup

  - **Estimated Time to complete**: 155 minutes

## Instructions

## Exercise 1: Evaluate your network with the Network Planner

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

In this exercise, you will determine if your organizations network has enough bandwidth to run Microsoft Teams successfully using Network Planner.

We will input our network details and review the output report.

### Task 1 - Create Personas

In the following task you will create a custom user persona of a network user. In our scenario we have some users that are expected to only use audio for p2p calls and PSTN calls. They will not use video or desktop sharing as part of their role. We need to create a persona to reflect their use when planning our network.

1. Sign into MS720-CLIENT01 as “Admin” with the password provided to you.

2. Open Microsoft Edge from the task bar and browse to the **Microsoft Teams admin center** at [**https://admin.teams.microsoft.com**](https://admin.teams.microsoft.com/).

3. You are still signed in as **MOD Administrator**. To follow the principal of least privilege, select the circle in the upper right-side corner and select **Sign out**.

4. Sign in with the credentials of **Katie Jordan**, the Teams Administrator for this lab.

5. Expand the left navigation menu, select and expand **Planning** and select **Network planner**.

6. Select **Personas**, you will see the default personas provided by Microsoft.

7. Select **Add**.

8. Enter a Persona name as **Audio Only User**.

9. Enter Description as **Audio Only User**.

10. Toggle **Audio**, **Conference audio** and **PSTN** to **On**.

11. Select **Apply**.

12. Leave this window open for the next Network planner task.

You have successfully created our Audio Only User network persona.

### Task 2 - Create Network and Network Sites

In this task you will setup your network and sites in Teams Network Planner. Contoso has 2 offices, Tacoma and Bellevue, so 2 network sites, we need to add to the planner

1. You are in **Network Planner** in the **Microsoft Teams admin center** on MS720-CLIENT01 as “Admin” and signed in as **Katie Jordan**.

2. Select **Network plans**.

3. You will see a prompt: “You haven't added any network plans yet.” Select **Add**.

4. Enter **Plan 1** for your name and **Plan 1** for your description and select **Apply**.

5. Once created select **Plan 1** in the list.

6. You will be prompted “You haven't added any network sites yet.” Select **Add a network site**.

7. Enter the **name** as **Tacoma** **Site**.

8. Enter the description as **Tacoma Office**.

9. You do not need to enter a street address, so skip **Create an address**.

10. Enter the **network users** as **50**, as we have 50 users in the Tacoma office.

11. Network subnets are just for reference in the report, our Tacoma offices network subnet is **10.10.1.0** with a network range of **24**. Enter these values.

12. Tacoma has local internet breakout, enter **50** for **Internet link capacity**.

13. It is not **connected to a WAN** or **ExpressRoute**, so leave those at the default of **off**.

14. There is no local PSTN on the Tacoma site, so leave **PSTN egress** as **Use VoIP only**.

15. Select **Save**.

16. Now select **Add network site** to add our second site, Bellevue.

17. Enter the **name** as **Bellevue Site**.

18. Enter the description as **Bellevue Office**.

19. You do not need to enter a street address, so skip **Create an address**.

20. Enter the **network users** as **90**, as we have 90 users in the Bellevue office.

21. Network subnets are just for reference in the report, our Bellevue offices network subnet is **10.10.20.0** with a network range of **24**. Enter these values.

22. Tacoma has local internet breakout, enter **20** for **Internet link capacity**.

23. It is not **connected to a WAN** or **ExpressRoute**, so leave those at the default of **off**.

24. There is no local PSTN on the Tacoma site, so leave **PSTN egress** as **Use VoIP only**

25. Select **Save**.

26. Leave this window open for the next Network planner task.

You have successfully added our two sites, user numbers and bandwidth details to network planner.

### Task 3 - Run Reports

In the following task you will run the Network Planner report and review the results.

1. You are in **Network Planner** in the **Microsoft Teams admin center** on MS720-CLIENT01 as “Admin” and signed in as Katie Jordan.

2. Select **Report**.

3. You will be prompted with “You haven't generated any reports yet.” Select **Start a report**.

4. Enter the report **name** as **Network Report 1**.

5. Enter a description of **Network report for Tacoma and Bellevue**.

For each site we must now define the number of users of each profile type. 

6. For **Tacoma Site**, in the **Office worker** row, set Network users to **30**.

7. Remove the **Remote Worker** row by selecting the **X** at the end of the row.

8. Click **+Add** and choose **Audio Only User** 

9. In the **Audio Only User** row, set Network Users to **20**.

10. For **Bellevue Site**, in the **Office worker** row, set Network users to **80**.

11. Remove the **Remote Worker** row by selecting the **X** at the end of the row.

12. Click **+Add** and choose **Audio Only User**

13. In the  **Audio Only User** row, set Network Users to **10**.

14. Now select **Generate report**.

15. Close the browser window at the end of the task.

You have successfully generated a Network Planner Report. We can see from the results that, at the default of 30% allowed bandwidth for Microsoft Teams reserved for real-time communications the Tacoma site is fine for bandwidth, but the Bellevue site does not have enough, as we can see by the figure highlighted in red. It would be recommended to increase the internet bandwidth at the Bellevue site.

## Exercise 2: Use the Teams Network Assessment Tool

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

In this exercise, you will install and run the Teams Network Assessment Tool to check the connectivity and performance from a client machine. This is an important task to understand if any network issues could probably degrade the user experience for Teams in your company and to develop strategies for optimizing your network.

### Task 1 - Install the Tool

In this task you will sign into a client machine provided by your training provider install the Teams Network Assessment Tool which is required to perform different tests.

1. Sign into MS720-CLIENT01 as “Admin” with the password provided to you.

2. Open Microsoft Edge from the task bar and browse to the following site: [**https://www.microsoft.com/en-us/download/details.aspx?id=103017**](https://www.microsoft.com/en-us/download/details.aspx?id=103017).

3. Select **download** to download the installer.

4. Go to **Start**, enter **Run** and select **Run**, and enter **Shell:Downloads** in the open dialog and select **OK**, this will open the downloads folder.

5. Find **MicrosoftTeamsNetworkAssessmentTool.exe**, right select it and run as administrator.

6. In the **User Account Control** window that asks “Do you want to allow this app to make changes to your device?”, select **Yes**.

7. The Microsoft Teams Network Assessment Tool Setup will start, select to tick **I agree to license terms and conditions** and select **Install**.

8. Select **Next** on the installer.

9. **Tick** to accept the terms in the license agreement and select **Next**.

10. Change the **destination folder** install path to **C:\NetworkTest**, select next.

11. Select **Install**.

12. Once the installer completes, select **Finish** to exit.

13. At the **Install successfully completed** prompt, select **Close**.

You have successfully installed the Teams Network Assessment Tool onto Client01.

### Task 2 - Run the Network Connectivity Check

The Teams Network Assessment Tool is run from the command line. We will now run the network connectivity check, which requires no command line switches. Firstly, the tool will check if it has connectivity to the Teams media relay. These are used to relay audio and video when direct connection between clients is not possible. The checker also checks whether the load-balancer relay is QoS (Quality of Service) capable, which means the load-balancer redirects packets to relay instance ports 3479-3481 (instead of 3478) depending on modality (audio = 3479, video = 3480, screenshare/data = 3481).

1. You are still signed in to MS720-CLIENT01 as “Admin” with the password provided to you.

2. Select **Start**, enter command prompt, find command prompt and right select it and chose **Run as administrator**.

3. At the “do you want to allow this app to make changes to your device” prompt, select **Yes**.

4. The command prompt will appear.

5. Type **cd C:\NetworkTest** and press enter, this changes our directory to the NetworkTest Directory.

6. Enter **NetworkAssessmentTool.exe** and press enter to run that program.

7. You will get a **Windows Defender Firewall Prompt;** Ensure Public networks is ticked and select **allow access**.

8. The test will complete, and you will see Service connectivity result has been written to: and a file path, and be put back at the command prompt.

You have started the Network Assessment Tool for the first time.

### Task 3 - Interpret Results of the Network Connectivity Check

In the following task you will read the results from the network connectivity check.:

1. You are still signed in to MS720-CLIENT01 as “Admin” and with the Network Assessment Tool open.

2. You can see from the command prompt output that the tests have been completed successfully, you can see:

	- Relay connectivity and QoS (Media Priority) check is successful for all relays.

	- Service verifications completed successfully.

You have successfully reviewed the results of the network connectivity check.

### Task 4 - Run the Network Quality Check

The network quality check (performance test) is run with the NetworkAssessmentTool.exe /qualitycheck switch. This will test sending real packets across the network.

1. You are still signed in to MS720-CLIENT01 as “Admin” with the command prompt running.

2. Enter **cd C:\NetworkTest** and press enter, this changes our directory to the NetworkTest Directory.

3. Enter **NetworkAssessmentTool.exe /qualitycheck** and press enter to run that program.

4. This will now run the test, you will see output come up on the command prompt, note you can see the **Loss Rate**, **Latency** and **Jitter** as the tests are performed.

5. The test will run for 300 seconds with tests every 5 seconds, we will finish the test early. After 10 or more tests have been completed, press **Ctrl+C** to stop the test.

6. When the test is complete, you will see the output **Call Quality Check Has Finished Call Quality Check result has been written to: C:\Users\LabUser\AppData\Local\Microsoft Teams Network Assessment Tool\\<Number\>quality_check_results.csv**

### Task 5 - Interpret Results of the Network Quality Check

In the following task you will review the results of the Network Quality Check.

- **Packet loss**: This is often defined as a percentage of packets that are lost in a given window of time. Packet loss directly affects audio quality—from small, individual lost packets having almost no impact to back-to-back burst losses that cause audio to cut out completely.

- **Latency:** This is the time it takes to get an IP packet from point A to point B on the network. This network propagation delay is essentially tied to physical distance between the two points and the speed of light, including additional overhead taken by the various routers in between. Latency is measured as one-way or round-trip time.

- **Inter-packet arrival jitter, or simply jitter:** This is the average change in delay between successive packets. Most modern VoIP software, including Skype for Business, can adapt to some levels of jitter through buffering. It's only when the jitter exceeds the buffering that a participant will notice the effects of jitter.

Review Packet Loss, Latency and Jitter by following these steps:

1. You are still signed in to MS720-CLIENT01 as “Admin” and at the command prompt.

2. Enter the following into the command prompt:

    ```console
    cd %userprofile%"\AppData\Local\Microsoft Teams Network Assessment Tool\"
    ```

3. Press **Tab** to tab through files in that directory, when you see a file name ending in _quality_check_results.csv press **Enter** to open the file. 

4. Select the top right X to close the activation prompt when excel loads. You can now see your test results in Excel.

5. Close Excel and the command prompt when complete

Microsoft’s performance targets for Teams are:

- **LossRate %**, also called Packet loss <0.1% during any 15s interval – the tests are 5 seconds each, so we should not be breaching this threshold

- **AverageLatency-Ms, (one way)** **&lt; 50ms**

- **AverageJitter-Ms, &lt;30ms during any 15s interval**

Note, due to performing the test on a lab VM, you may see unusual or high results, especially with latency.

At the end of this task, you have successfully reviewed the results of the Network Quality Check.

## Exercise 3: Configure a basic network topology for dynamic emergency calling 

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

Network sites are used for Dynamic emergency calling. Before configuring dynamic emergency calling we must map the relevant Network Regions, Network sites, network subnets and Trusted IP addresses. In this exercise we will configure a network region and sites

### Task 1 - Add Network Region and sites to Network Topology

In this task you will sign into client01 and the Teams Admin Center and add our two offices as Network Sites in Network Topology

1. Sign into MS720-CLIENT01 as “Admin” with the password provided to you.

2. Open Microsoft Edge from the task bar and browse to the **Microsoft Teams admin center** at [**https://admin.teams.microsoft.com**](https://admin.teams.microsoft.com/).

3. Sign in with the credentials of the Teams Administrator for this lab, **Katie Jordan**.

4. Expand the left navigation menu and select to expand **Locations**, then select **Network topology**.

5. You will be prompted with **You haven't created any network sites yet**. Select **Add**.

6. Enter the **name** for the first Network Site as **Tacoma Network Site** and **Description** as **Tacoma Office**.

7. Select **Add a Network Region**, enter **UK** and select **Add**.

8. Select UK (select the circle) then select **Link**.

9. Select **Add subnets**.

10. Leave IP version as IPv4 and enter IP address as **10.10.10.0** with network range as **24**.

11. For Description enter **Tacoma Subnet**.

12. Select **Apply**.

13. You have now added a subnet for the Tacoma site, select **Save** to save the Tacoma site, note you may need to scroll down the page.

14. You can now see the Tacoma Network Site in the Network Sites List.

15. To add the Bellevue site select **Add**.

16. Enter the **name** for the first Network Site as **Bellevue Network Site** and **Description** as **Bellevue Office**.

17. Select **Add a Network Region**, select **UK** and select **Link**.

18. Select **Add subnets**.

19. Leave IP version as IPv4 and enter IP address as **10.10.20.0** with network range as **24**.

20. For Description enter **Bellevue Subnet**.

21. Select **Apply**.

22. You have now added a subnet for the Bellevue site, select **Save** to save the Tacoma site, note you may need to scroll down the page.

23. You can now see the Bellevue Network Site in the Network Sites List.

24. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have now added our 2 network sites, Tacoma, and Bellevue.

### Task 2 - Add a trusted IP address

In this task you will add a trusted IP addresses for each the Tacoma and Bellevue Offices. Trusted IP address are the enterprises public external IP addresses that a Teams user will show as routing from on the public internet. These are important as they validate that the user is on an enterprise network and the system should check if they are on a mapped subnet. We have two offices, each with their own internet connection and therefor public IP address. You do not need to map Trusted IPs to specific networks.

1. From the last task you are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams Admin Center** open as **Katie Jordan**.

2. On **Network topology**, select the **Trusted IPs** tab.

3. You will see “You haven't added any trusted IP addresses yet”. Select **Add**

4. You can add a specific IP or a subnet of public IPs, For the Bellevue office add **151.101.128.81** and **32** as the network range and in the description enter **Bellevue Office Public IP**.

5. Select **Apply**.

6. Select **Add** to add our second Public IP address.

7. For the Tacoma office add **151.101.128.91** and **32** as the network range and in the description enter **Tacoma Office Public IP**.

8. Select **Apply**.

9. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have successfully added the public IP that clients will appear from for the Tacoma and Bellevue Offices as Trusted IPs.

### Task 3 - Add an emergency address

In this task you will create an emergency location. This is needed before you can order calling plan numbers.

1. From the last task you are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams Admin Center** open as **Katie Jordan**.

2. Select the **Locations** then **Emergency addresses**.

3. On the toolbar, select the **Add**.

4. In the New Address pane, add a name for your Emergency address, **Bellevue Office Address**.

5. Select the **Country or region** menu and then select **United States**.

6. Switch **Input address manually** from Off to **On**.

7. In the **Street Number** box, enter **700**.

8. In the **Street Name** box, enter **Bellevue Way Northeast**.

9. In the **City** box, enter **Bellevue**.

10. In the **State** box, select **Washington**.

11. In the **Zip code** box, enter **98004**.

12. For Latitude enter **47.61676**.

13. For Longitude enter **-122.20083**.

14. Leave organization name as Contoso.

15. For ELIN enter **425-555-1200**.

16. Tick the **I acknowledge and agree…** checkbox under **Emergency calling disclaimer**.

17. On the new **Important Information** window select **Cancel**.

18. Select **Save**.

19. In the **Emergency locations** list verify your emergency location is listed and has been validated.

20. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have successfully added an emergency address

### Task 4 - Mapping a network to a physical location (emergency address)

Now that we have added our network Region, Sites and Subnets we can map our network locations to physical office addresses for emergency calling. 

TIP: This configuration refers to Emergency Locations, but when you are defining them, the Teams Admin Center calls them Emergency Addresses. They are the same thing.

You can map emergency location\addresses to:

- Wireless Access Point (WAP) by BSSID (Basic Service Set Identifier) - Each AP has a BSSID.

- Ethernet switch by Chassis ID. Each network switch is stamped with a Chassis ID that is used to identify a specific switch on a network.

- Ethernet switch port, which maps both the Chassis ID and the port ID. This allows a switch that spans multiple locations to be more accurately mapped down to the port.

- Subnet. Not tied to any physical equipment address, this is the network address the user has. Unlike mapped subnets in the Teams Network topology, The Location Information Service (LIS) doesn’t maintain a list of Networks and Subnet masks, it relies on the NetworkID of the subnet.

Perform the following steps.

1. From the last task you are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft** **Teams Admin Center** open as **Katie Jordan**.

2. Navigate to **Locations** and **Networks &amp; locations**.

3. We are going to map our office **Subnets;** ensure you are on the Subnets tab and select **Add** to add a subnet and Emergency Location.

4. Leave IPv4 Selected for **IP Version**.

5. Enter the Bellevue Subnet network ID, since our Bellevue Office subnet is 10.10.20.0/24, the network ID is **10.10.20.0**.

6. Do **not** set a description (there is a bug which stops the UI working when you add a description)

7. Under Emergency location, **Search by City** enter **Bellevue** and select our Bellevue emergency address.

8. Select **Apply**.

9. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have aligned a network subnet to a physical emergency address.

### Task 5 - Configure Emergency Calling Policies

In this task you will configure an emergency calling policy. Emergency calling policies define what happens when a user in your organization makes an emergency call. We would like Alex Wilber to receive a notification whenever an emergency call is made.

1. From the last task you are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams Admin Center** open as **Katie Jordan**.

2. In the left navigation pane select **Voice** and **Emergency polices**.

3. Select **Add** to add an Emergency Policy.

4. For **Name** enter **Contoso Emergency Policy**.

5. For **Description** enter **Contoso Emergency Policy**.

6. Under **Notification mode**, select **Send notification only**: A Teams chat message is sent to the users and groups that you specify.

7. In **Users and groups for emergency calls notifications**, enter Alex and then select Alex Wilber and select **Add**.

8. Select **Apply**.

9. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have successfully setup notifications for Alex Wilber whenever emergency calls are made.

## Exercise 4: Configure voice policies

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

In this exercise, you will configure some key voice setting and policies required for the Contoso users to utilize voice services in context with the company policies.

### Task 1 - Create a Dial Plan for extension dialing

In this task you will sign into the Client01 and the Teams Admin Center and configure a dial plan. Our Tacoma office users are used to using 3 digit short codes to call users internally, from 500 to 550. These 3 digit codes map 1:1 to the last 3 digits of their PSTN number. In Tacoma the numbers are +44208 566 5xx. XX represents 00 to 99, We own this number range for the Tacoma users.

So, for example, if a user’s phone number is +44208 566 511, employees are used to being able to dial 511 to ring that user.

We need to create a dial plan for Tacoma users to enable that scenario. While it is primarily Tacoma users who use this 5xx extension dialing, the organization has asked that Bellevue users should also be able to use the same extensions to dial Tacoma users. 

Since we want all users to be able to do 5xx extension dialing, we will add a new normalization rule to the Global dial plan, as this applies to all tenant users by default. If you only wanted to have the rule apply to selected users, you could create a specific dial plan and assign it to those users.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. In the left navigation pane expand **Voice** then select **Dial plans**. 

3. Select the **Global (org wide default)** dial plan.

4. Under Normalization rules you will see “You don't have any normalization rules yet”, select **Add** to get to the add new rule dialogue.

5. For **Name** enter **Tacoma 5xx extension dialing**.

6. For **Description** enter **Converts 5xx dialed extensions to full E.164 +44208 566 5xx number**.

7. Ensure **Basic** rule is selected, it should be by default.

8. Tick **The number dialed begins with** and enter **5**.

9. Tick **The length of the number being dialed is** and enter **3**.

10. Ensure **Exactly** is selected for length of number to be dialed.

11. Tick **Remove this many digits from the start of the number** and enter **1**.

12. Tick **Add this number to the beginning** and enter **+442085665**.

13. Test the rule by entering **503** and selecting **Test**. The output should be +44208566503, if the output is correct select **Save**.

14. You will see your rule as rule 1 in the global dial plan, select **Save**.

15. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

You have successfully added a normalization rule to a dial plan to meet the extension dialing organizational requirement.

### Task 2 - Configure Calling policies

Calling policies are used to control which features are available to users. By default, when a user is on a Call in Teams, a second call coming in will alert them with a toast, giving them the option to pick up the second incoming call. Our organization does not want users interrupted when they are on calls. This feature is called “busy on busy”.

At Contoso you need to enable the option of convenience recording 1:1 calls, which is disabled by default. Your labs Teams Administrator, Katie Jordan will create a custom calling policy and apply it to all users via a Group policy assignment.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. In the left navigation menu select **Voice** and **Calling policies**. 

3. Select **Add** to add a new policy.

4. Under add a **name** for your calling policy enter **Busy on busy and call recording**.

5. Under add a **friendly description** enter **Busy on busy and allow call recording**.

6. Switch **Cloud recording for calling** to **On**.

7. For **Busy on busy when in a call** to **Enabled**.

8. Select **Save**.

9. While still in Voice and calling policies, select the **Group policy assignment** tab.

10. Select **Add group** to open the **Assign policy to group** dialogue.

11. For Select a group enter **all company** and when all company group appears select **Add**.

12. Leave rank as 1.

13. For select a policy select the new **Busy on busy and call recording** policy.

14. Select **Apply**.

15. Leave the browser open in the Microsoft Teams admin center at the end of this task.

The policy is now applied to all users in the default **all company** group. If a user is directly assigned a policy (either individually or through a batch assignment), that policy takes precedence over a policy inherited by being a member of a group. This leaves the option for specific users to be directly assigned a different policy should they want busy on busy disabled.

You have successfully created and assigned a calling policy.

### Task 3 - Configure Call Park policies

Call Park and retrieve lets users put calls on hold and enables the same user or someone else to retrieve and continue the call.

Call Park is disabled by default. Our organization would like the option to use call park so we will enable it.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. In the left navigation menu select **Voice** and **Call park policies**. 

3. Select the **Global (org wide default)** policy.

4. Switch **Call park** to **On**.

5. Select **Save**.

6. Leave the browser open in the **Microsoft Teams admin center** at the end of this task.

The call pickup range is from 10 to 99 and cannot be customized. You have successfully enabled call park for all users.

### Task 4 - Configure Caller ID policies

Caller ID policies are used to change or block the Caller ID or phone number presented when making or receiving PSTN calls.

By default, the user's phone number is displayed when an outbound call is made to a PSTN phone number such as a landline or mobile phone. In most cases most companies will be happy with this default. Some users in our organization do not want their number presented when they make outbound PSTN calls. In this task we will create a Caller ID policy to block the presentation of any PSTN number, ready to be assigned to those users.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Select **Voice** and **Caller ID policies**.

3. Select **Add**.

4. For **name** enter **Block outbound caller ID**.

5. For **friendly description** enter **Block outbound caller ID**.

6. Switch **Override the caller ID policy** from Off to **On**.

7. For **Replace the caller ID with** select **Anonymous**.

8. Select **Save**.

9. Leave the browser window open at the end of this task.

You have successfully created a caller ID policy to block the outgoing caller ID for users.

### Task 5 - Configure Inbound call blocking

There is a persistent nuisance caller calling users in the Bellevue office and we need to block all inbound calls from that number for the organization. The calling number is 1 (412) 555-1111.

1. You are still signed in to MS720-CLIENT01 as “Admin” with the password provided to you.

2. Press the start button and enter PowerShell.

3. Windows PowerShell will appear on the start menu, right click on it and select **Run as administrator**.

4. Windows PowerShell will load, enter the following at the command to connect to Microsoft Teams.

    ```powershell
    Connect-MicrosoftTeams
    ```

5. It may take around a minute to connect, when prompted enter the username of **Katie Jordan** and select **Next**.

6. When prompted enter the password of the M365 Tenant Administrator and select **Sign In**.

7. When signed in you will be returned to the command prompt.

8. Run the following to block incoming calls.

    ```powershell
    New-CsInboundBlockedNumberPattern -Name "BlockNusance1" -Enabled $True -Description "Block Fabrikam" -Pattern "^\+?14125551111"
    ```

9. Close the PowerShell window at the end of the task with the **X** in the upper right-side corner.

You have successfully blocked all inbound calls from 1 (412) 555-1111 via PowerShell to end the unwanted calls from that number. 

## Exercise 5: Prepare users for calling

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

In this exercise, you will setup a user for Teams Phone with a Microsoft Calling plan. 

### Task 1 - Order a phone number

In this task you will order a phone number in the Teams Admin Center to assign to Isaiah Langer.

1. You are still signed in to MS720-CLIENT01 as “Admin” and in the **Microsoft Teams admin center** as **Katie Jordan**

2. In the **Microsoft Teams admin center**, select **Voice** on the left menu, then select **Phone numbers**.

3. Under **Numbers**, select **Add**.

4. At the top of the page, enter a name for your order **Bellevue numbers for users**.

5. For friendly description enter **Bellevue user numbers order**.

6. Select **United States** as **Country or region**.

7. For Number Type, select User (subscriber).
						
8. For Operator, select Microsoft.						

9. The Quantity field will now appear, enter 1.

10. For **Search for new numbers** select **Search by area code** and enter **206**.

**Note**: The phone numbers that are available in different regions will vary and **206** numbers may not be available. Try other area codes in the US and Canada, such as **308** in Nebraska.  The area code of the phone number does not need to match the emergency address location.

11. When all fields are complete, select **Next**. Microsoft will now reserve phone numbers in the chosen area code. If there are no numbers available for your selected State/City combination, select another State/City and try again.

12. Verify the area code and phone number, then select **Place Order**.

13. You will see “Thank you, your order has been placed!”, select **Finish**.

14. In the voice, under **phone numbers**, you should see your number. Note in some cases this may take 5-10 minutes to appear.

15. Leave the browser window open at the end of the task.

You have successfully ordered a phone number through the Teams admin center.

### Task 2 - Assign a phone number to Isaiah Langer

Before a user can make calls, they need a phone number. In this task you will assign the phone number you ordered earlier to Isaiah Langer.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams** **admin center** open as **Katie Jordan**.

2. Select **Voice** and the **Phone numbers** tab.

3. Select the new phone number we ordered in Task 1.

4. Select **Edit** from the top table menu.

5. Enter **Isaiah Langer** in the **Assigned To** field, then select **Assign**.

6. Under **Emergency location**, select **Search by city**, and then enter **Bellevue** and select the address you verified earlier.

7. Select **Apply**.

8. The phone number is now assigned to Isaiah. Close the browser window at the end of the task.

You have successfully assigned a phone number to Isaiah Langer.

### Task 3 - Test phone calls

Now Isaiah has a calling plan and phone number and we will perform a test call to validate functionality of the configuration.

1. Switch to MS720-CLIENT02 and sign in as “Admin” with the credentials provided to you.

2. Open the Edge browser and navigate to [https://teams.microsoft.com](https://teams.microsoft.com/). Sign in with the credentials of Isaiah.

3. Log in as Isaiah Langer using the password you assigned in the previous lab. When a **Save password** dialog is displayed, select **Never**.

4. When a **Stay signed in?** dialog is displayed, select **No**.

5. Close the **Bring your team together** message and select the download button in the lower left-side of the window.

6. When the download has finished, select **Open file** below **Teams_windows_x64.exe**.

7. Select **Get started**.

8. When prompted for sign in, enter Isaiah Langer’s username.

9. When prompted enter Isaiah Langer’s password reset in a previous exercise.

10. You will be prompted with “Stay signed into all your apps” select **No, sign in to this app only**.

11. If you are prompted with the Teams welcome information:

	- Bring your team together, select **Next**.

	- Chat 1:1 and with groups, select **Next**.

	- Connect through online meetings, select **Next**.

	- Files, notes, apps, and more, all in one place, select **Next**.

	- You're ready!, select **Let’s go**.

12. If you are prompted **Get the Teams mobile app**, select the top right X to close the prompt.

13. Select the **Calls** button on the left rail.

14. Dial +18776967786 and press call.

15. If your lab machine prompted, you to use your microphone select **Allow**.

16. If you are prompted by Windows Defender Firewall for Microsoft Teams select **Allow Access**

17. Note the call connects.

18. Press the red hang-up button to disconnect the call.

Now we confirmed that Isaiah can make a PSTN call in Teams

## Exercise 6: Configure audio conferencing settings

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will configure Microsoft PSTN audio conferencing to meet the organizations requirements.

### Task 1 - Set a default Audio Conferencing Bridge

The default phone number of your conference bridge defines the caller ID that will be used when an outbound call is placed by a participant or the organizer from within a meeting. E.g., they are dialing out to either connect themselves via PSTN or to “dial in” another participant on PSTN.

Contoso does a lot of work with companies in New York and would prefer a New York number is their default audio conference bridge.

1. Switch back to MS720-CLIENT01 and sign in as “Admin” with the password provided to you.

2. Open Microsoft Edge from the task bar and browse to the **Microsoft Teams admin center** at [**https://admin.teams.microsoft.com**](https://admin.teams.microsoft.com/).

3. You are still signed in as the Teams Administrator Katie Jordan.

4. Navigate to **Meetings** on the left menu then **Conference bridges**.

5. You will see all the conference bridge numbers listed; one number will have (Default) beside it. That is the current default.

6. Select Location in the top table menu to sort the Locations in the table alphabetically, scroll down to find the New York City, United States number, select to highlight it and select the **Set as default** on the top menu.

7. Leave the browser window open at the end of the task.

You have successfully set a New York City, United States number as the default audio conference number.

### Task 2 – Order a new Conference Bridge Number

Contoso would like to have a conference number for their customers to dial into specifically in the United States 920 area code. In this task we will order that number and add it to our tenant.

In this task you will order a new Dedicated conference bridge toll number. This will be a dedicated number for people to dial into Contoso conferences.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Navigate and select **Voice** on the left menu, then select **Phone numbers**.

3. Under **Phone numbers**, select the **Add**.

4. At the top of the page, enter a name for your order **Dedicated conference number**.

5. For friendly description enter **Dedicated conference number**.

6. Select United States as **Country or region**.

7. For **Number Type**, select **Dedicated conference bridge (Toll)**.

8. Select **Microsoft** in the Operator field, the Quantity field will now appear, enter 1.

9. For **Search for new numbers** select **search by area code** and enter **920**.

10. When all fields are complete, select **Next**, Microsoft will now reserve and present some numbers for you. If you see “We can't find any phone numbers for the area code you entered.” Try another US area code for this exercise. If you really did want a specific city, you would contact the PSTN service desk to find out if/when there is availability.

11. You should see 1 reserved number, select **Place Order**.

12. You will see “Thank you, your order has been placed!”, select **Finish**.

13. In the voice, under **Phone numbers**, you should see your number. Note in some cases this may take 5-10 minutes to appear.

14. Leave the browser window open at the end of the task.

You have successfully ordered a new dedicated conference toll phone number through the Teams admin center.

### Task 3 - Configure a New Conference Bridge Number

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. In the left navigation menu select **Meetings** and **Conference bridges**. 

3. Select **Add** and select **Toll number**. 

4. Select the new conference number you acquired in task 2.

5. Select **Apply**.

6. You will be back at the list of conference bridge numbers, sort the list by type to confirm you have a new Dedicated conference bridge. It may take a few minutes for the bridge to appear. You can refresh the page by moving to a different page in the Teams Admin Center then returning to the **Conference bridges** page.

7. Leave the browser window open at the end of the task.

You have successfully setup a new dedicated conference bridge number.

## Exercise 7: Configure call queues and auto attendants

### Exercise Duration

  - **Estimated Time to complete**: 45 minutes

In this exercise, you will gain an understanding of how to configure Call Queues and Auto Attendants. Auto attendant being configured today is for the Sales Team. The sales team take sales queries and then apply them to different parts of the business. On this occasion Alex Wilber is going to be part of the call queue and later in the module we will see how to then assign it to a Team.

### Task 1 - Create a call queue in the Teams Admin Center

In this task you will create a call queue. A call queue is a group of agents that you can direct calls to.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Select **Voice** and then select **Call queues**.

3. Select **Add** and enter the **Sales CQ** as the name

4. Under **Resource accounts**, select **Add**.

5. Enter **Sales** in the search box, when no results are found, select **Add resource account**.

6. Enter **Sales CQ** as **Display name**

7. **SalesCQ** as **Username,** leave domain as is, 

8. **Resource account type** select **Call queue**, then select **Save**.

9. Once saved, you will see Sales CQ under accounts to add, select **Add**.

10. You do not need to assign a Calling ID for this lab

11. Set **Language** to **English (United States)**.

12. Under **Call answering** select **Choose users and group, Add users**, search for Isaiah Langer. and select **Add**.

13. Leave the other options as default

14. Scroll down the page and select **Submit**. You will see your call queue in the call queues list

15. Leave the Teams Admin Center Open for the next steps

You have successfully created the Sales CQ call queue and added Isaiah Langer as an agent

### Task 2 - Create an auto attendant for the Sales call queue

Now we will create an auto attendant and direct one of the options to send calls to our Sales CQ call queue. This will ready the Microsoft 365 Auto Attendant to become functional. 

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Under **Voice**, select **Auto Attendants** and select **Add**.

3. Enter **Sales AA** for the name, 

4. Time zone of **(UTC-08:00) Pacific Time (US…)**,

5. Leave the Language as default

6. select **Next**.

7. Under **Call flow**, select **Add a greeting message** and enter, “Thank you for calling Contoso, your call is important to us, please be patient while we handle your call”.

8. Under **Call routing options**, select **Redirect Call**, then select Redirect to **Voice App**, enter **Sales CQ**, then select **Next**

9. Under **Set business hours** leave the defaults and select **next**, 

10. Under set Holiday call settings select **Next**, 

11. Under Dial scope select **Next**.

12. Under **Resource Accounts**, Select **Add**, enter **Sales AA** in the search box, then select **Add Resource Account**, enter **Display Name** of **Sales AA**, Username is **SalesAA**, and **Resource account type** of **Auto Attendant**, select **Save**.

13. Select **Add**, select **Submit** under **Resource Accounts** menu.

14. You will see your Sales AA auto attendant in the auto attendants list

15. Leave the Teams Admin Center open for the next task

You have successfully created an Auto Attendant, and aligned it to a Call Queue

### Task 3 – Configure a Call Queue to use a channel

Collaborative calling enables you to connect a call queue to a channel in Teams. Users can collaborate and share information in the channel while taking calls in the queue. Instead of defining the agents in the Teams Admin Center, the agents are defined by who is members of the team.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Under **Voice**, and **Call Queues**, select **Sales CQ**.

3. Under **Call answering** select **Choose a team**, select **Add a channel**. 

4. Type **Contoso**, select the channel and select **Add**, select **General**, select **Apply**.  

5. Leave the Teams Admin Center open for the next task

You have successfully assigned the call answering for the Call Queue to the General channel within the Contoso team.

### Task 4 - Configure a Call Queue to forward to voicemail if busy

By default, if a call to a call queue isn't answered by an agent within the maximum wait time, it will be disconnected. We would like to configure unanswered calls to go to voicemail instead. The voicemail must be an Office 365 Group voicemail.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Under **Voice**, and **Call Queues**, select **Sales CQ**

3. Under **Call time out handling**, select **Redirect this call to**, select Redirect to, from the drop-down menu select **Voicemail (Shared)**

4. In the search type **All**, select **All Company**, 

5. Set Enable **Transcription On**

6. Select **Add a greeting message** and type **“we are unable to take your call, please leave a message and we will be back with you as soon as possible.”** 

7. Select **Submit**

You have successfully assigned a voicemail to the Call Queue should it reach a time out period. 

### Task 5 - Explore conference mode toggle

In this task you will enable conference mode that will then make it pass the call between the inbound calls more quickly.

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Under **Voice**, and **Call Queues**, select **Sales CQ**, 

3. Under **Call answering** select find **Conferencing mode**, toggle the setting to **On**. 

4. Click **Submit**.

You have successfully enabled conferencing mode for **Sales CQ** call queue.

### Task 6 - Set holiday modes within AA

In this task you will create the relevant holiday configuration. Holidays differ from country to country but in this instance, we will just create a new holiday time that’s relevant to yourself. 

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

1. In the Microsoft Teams admin center, go to **Voice &gt; Holidays**.

2. Select **Add** to start the creation of a new holiday.

3. Enter a name for the holiday.

4. Select **Add new date**.

5. Under **Start time**, select the calendar icon and choose the date when you'd like the holiday to begin.

6. Use the drop-down list to select a start time for the holiday.

7. Under **End time**, select the calendar icon and choose the date when you'd like the holiday to end.

8. Use the drop-down list to select an end time for the holiday. **The End** time must be after the **Start time**.

9. Optionally, add more dates for recurring holidays.

10. Select **Save**.

You have successfully created a holiday relevant to your area and assigned it to a Call queue. 

### Task 7 - Import MP4 file in as custom music on hold

In this task you will obtain a free MP3 to the music on hold solution for the Sales Call Queue

1. You are still signed in to MS720-CLIENT01 as “Admin” and have the **Microsoft Teams admin center** open as **Katie Jordan**.

2. Open Microsoft Edge open a new tab and browse to [https://onhold2go.co.uk/Free_Music_On_Hold.php](https://onhold2go.co.uk/Free_Music_On_Hold.php).

3. Download **A New Life** by selecting the **Download test file**. If the Edge browser indicates the file is insecure, select the ellipses, then select Keep. Select **Keep anyway**. Once the zipped file is downloaded, open the downloads folder and extract the files contained within it. Extract them into the Downloads folder.

4. Close the tab and switch back to the Microsoft Teams admin center.

5. Under **Voice** and **Call Queues**, select **Sales CQ**.

6. to go into edit mode by double clicking **Sales CQ**.

7. Under **Music on hold**, select **Play an audio file**.

8. Select **Upload file**, navigate to the **Downloads** folder, select **A-New-Life.mp3** and select **Open**.

9. Select **Submit**.

10. Select the circle with the KJ initials in the upper right-side and select **Sign out**.

11. Close all browser windows currently open.

You have successfully signed into your test clients and assigned a new MP3 file to the call queue.
