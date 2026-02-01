# Identity-and-Access-Management-IAM-Project

## Objective



### Skills Learned



### Tools Used



## Steps

1. First I will create a tenant in Microsoft Entra ID as it is the central identity authority for my Azure environment.
   
   <img width="2558" height="591" alt="1" src="https://github.com/user-attachments/assets/bd3cdfd1-320b-456f-aeb3-94a6f0fd50b2" />

3. I have decided to make two break-glass accounts to add redundancy and prevent a single point of failure. These accounts are special accounts that are excluded from normal security policies like conditional access and MFA, in case they get misconfigured and block everyone out. They are to be used in emergencies only.

   <img width="2553" height="490" alt="2" src="https://github.com/user-attachments/assets/9cb784ac-4cfe-4fb8-b3aa-28d8ba183453" />

5. I am now adding users to simulate real people accessing the cloud resources.
   
   <img width="2559" height="672" alt="3" src="https://github.com/user-attachments/assets/18b29447-9655-431d-8f05-24b8a77257fe" />

7. Now I am making security groups and putting appropriate users into their respective groups. Group-based access lets you manage permissions at scale while limiting privilege creep and upholding least privilege.
  
   These groups are dynamic and work by automation. These work by automatically putting you in a group based on the attributes that you can set. For example, one of my users department is Finance, and using this dynamic query (user.department -eq "Finance") it will automatically put this user in the Finance-Users security group.
   
   <img width="2555" height="601" alt="4" src="https://github.com/user-attachments/assets/700ce324-6618-4918-b6fb-6f0804ace0ef" /> 

9. Here, I have given the Microsoft Entra P2 license to these groups. Giving licences to groups instead of by user is way more efficient and effective, simplifying licence management for scalability.
   
    <img width="2559" height="787" alt="5" src="https://github.com/user-attachments/assets/c19ea421-825e-473d-9653-68b5be7e5657" />

10. I have created more groups, and I am going to assign Azure AD/Entra roles to them. I have given IAM-Readers the Global reader role to allow auditing and reporting without risking accidental changes.
   
    Next, I have given IT-User-Admins the User Administrator role to be able to create, update, delete users and groups, and reset passwords.

    Lastly, for the Security-Readers, I have given them the Security Reader role to read security reports, alerts, and conditional access policies without being able to change any security settings.

    This is a great way to use least privilege principle and separation of duties.

    <img width="2559" height="724" alt="6" src="https://github.com/user-attachments/assets/bc3549ac-70d5-47f5-b8db-6e4d301ec617" />

12. In this screenshot, I have added an IAM test user to the IAM-Readers group. Now this user will have Global Reader access.
    <img width="2557" height="660" alt="7" src="https://github.com/user-attachments/assets/76d3cc1e-ba34-4839-8580-731efbaf5e65" />

13. I have set up a resource group to manage access using groups instead of assigning roles to individual users.

    KY-IAM-Admin, which has the Owner Role, has full control over resource groups, useful for managing the resources
    KY-IAM-Contributors, which has the Contributor role, can create and manage resources, but cannot assign roles, useful for developers to work safely and prevent privilege escalation.
    KY-IAM-Readers, which have the Reader role, has read only access to resources in the resource group, useful for auditing and monitoring.
    
    <img width="2555" height="493" alt="8" src="https://github.com/user-attachments/assets/8f8d1918-da89-403f-9f9f-8b571092b6fc" />

15.  
    <img width="2529" height="448" alt="9" src="https://github.com/user-attachments/assets/60dde71d-21f9-49bc-aa5d-fe0f28cae9bb" />

16.
    <img width="2555" height="761" alt="10" src="https://github.com/user-attachments/assets/3b33fae6-1ee1-49a5-aeb0-c8626277d906" />

17.
    <img width="2540" height="487" alt="11" src="https://github.com/user-attachments/assets/c6c1d352-7b8a-4268-a869-893aec51daa9" />

18.
    <img width="2557" height="519" alt="12" src="https://github.com/user-attachments/assets/d381ab89-9016-4595-b463-efb563b0c651" />

19.
    <img width="2554" height="549" alt="13" src="https://github.com/user-attachments/assets/5ffe1482-9c8b-49ed-8858-d9a7411cd8d2" />

20.
    <img width="2559" height="580" alt="14" src="https://github.com/user-attachments/assets/45ccc8bf-032e-4739-8788-d31d3e488dce" />

21.
    <img width="2559" height="746" alt="15" src="https://github.com/user-attachments/assets/f78bdb09-5d65-4936-88b4-3efdcc69fc70" />

























