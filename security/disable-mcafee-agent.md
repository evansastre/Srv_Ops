# Disable McAfee Agent



**Batch Disable**

1. Login ePO server, open ePO admin site
2. Policy Catalog → Product: McAfee Agent, Category: General → My Default → General → Uncheck the "Enable self protection \(Windows only\)"
3. Send a wake up agent call. Once the wake up agent call gets triggered successfully the policy will get applied to the machine and after that you will be able to disable the service. 

**One Machine Disable**

1. Login ePO server, open ePO admin site
2. System Tree → Tick the target server → Actions → Modify Policies on a Single System → McAfee Agent → Category: General, Policy: My default → Duplicate the policy and give name to the policy \(e.g. Disable McAfee Agent\) and make the changes: Untick the "Enable self protection \(Windows only\)" → Save the policy
3. Click on the "Edit Assignment" of "Category: General, Policy: My default" → Select the option "Break inheritance and assign the policy and settings below" → From the from the drop down please select the duplicated policy \(e.g. Disable McAfee Agent\)
4. Once the policy get saved, send a wake up agent call to the machine and after that you will be able to disable the McAfee Agent Services.

