# Identity-and-Access-Management-IAM-Project

## Objective
The objective of this project is to implement and manage a strong Identity and Access Management (IAM) system within the Microsoft Azure cloud environment. The project aims to ensure that users, groups, and applications have appropriate and secure access to organizational resources while minimizing security risks and maintaining operational efficiency.


### Skills Learned

Azure Active Directory (Azure AD): Configuring users, groups, and applications.

Role-Based Access Control (RBAC): Designing and implementing access policies for secure resource management.

Authentication & Security: Implementing Multi-Factor Authentication (MFA) and conditional access policies.

Identity Lifecycle Management: Managing onboarding/offboarding, role changes, and automated provisioning of accounts.


### Tools Used

Microsoft Entra ID

Azure Active Directory (Azure AD)

Azure Role-Based Access Control (RBAC)

Azure MFA (Multi-Factor Authentication)

Privileged Identity Management (PIM)

Azure Conditional Access

Azure AD Identity Protection








# Steps

## Create / Verify Entra ID Tenant


1. First I will create a tenant in Microsoft Entra ID as it is the central identity authority for my Azure environment.
   
   <img width="2558" height="591" alt="1" src="https://github.com/user-attachments/assets/bd3cdfd1-320b-456f-aeb3-94a6f0fd50b2" />

## Identity Setup

2. I have decided to make two break-glass accounts to add redundancy and prevent a single point of failure. These accounts are special accounts that are excluded from normal security policies like conditional access and MFA, in case they get misconfigured and block everyone out. They are to be used in emergencies only.

   <img width="2553" height="490" alt="2" src="https://github.com/user-attachments/assets/9cb784ac-4cfe-4fb8-b3aa-28d8ba183453" />

3. I am now adding users to simulate real people accessing the cloud resources.
   
   <img width="2559" height="672" alt="3" src="https://github.com/user-attachments/assets/18b29447-9655-431d-8f05-24b8a77257fe" />

## Role-Based Access Control (RBAC)

4. Now I am making security groups and putting appropriate users into their respective groups. Group-based access lets you manage permissions at scale while limiting privilege creep and upholding least privilege.
  
   These groups are dynamic and work by automation. These work by automatically putting you in a group based on the attributes that you can set. For example, one of my users department is Finance, and using this dynamic query (user.department -eq "Finance") it will automatically put this user in the Finance-Users security group.
   
   
   <img width="2555" height="601" alt="4" src="https://github.com/user-attachments/assets/700ce324-6618-4918-b6fb-6f0804ace0ef" /> 

5. Here, I have given the Microsoft Entra P2 license to these groups. Giving licences to groups instead of by user is way more efficient and effective, simplifying licence management for scalability.
   
    <img width="2559" height="787" alt="5" src="https://github.com/user-attachments/assets/c19ea421-825e-473d-9653-68b5be7e5657" />

6. I have created more groups, and I am going to assign Azure AD/Entra roles to them. I have given IAM-Readers the Global reader role to allow auditing and reporting without risking accidental changes.
   
    Next, I have given IT-User-Admins the User Administrator role to be able to create, update, delete users and groups, and reset passwords.

    Lastly, for the Security-Readers, I have given them the Security Reader role to read security reports, alerts, and conditional access policies without being able to change any security settings.

    This is a great way to use least privilege principle and separation of duties.

    <img width="2559" height="724" alt="6" src="https://github.com/user-attachments/assets/bc3549ac-70d5-47f5-b8db-6e4d301ec617" />

7. In this screenshot, I have added an IAM test user to the IAM-Readers group. Now this user will have Global Reader access.
    
    <img width="2557" height="660" alt="7" src="https://github.com/user-attachments/assets/76d3cc1e-ba34-4839-8580-731efbaf5e65" />

8. I have set up a resource group to manage access using groups instead of assigning roles to individual users.

    KY-IAM-Admin, which has the Owner Role, has full control over resource groups, useful for managing the resources
    
    KY-IAM-Contributors, which has the Contributor role, can create and manage resources, but cannot assign roles, useful for developers to work safely and prevent privilege escalation.
    
    KY-IAM-Readers, which have the Reader role, has read only access to resources in the resource group, useful for auditing and monitoring.
    
    <img width="2555" height="493" alt="8" src="https://github.com/user-attachments/assets/8f8d1918-da89-403f-9f9f-8b571092b6fc" />

## Multi-Factor Authentication (MFA)    

9. Here I am enforcing Multifactor authentication for all users
    
    <img width="2555" height="761" alt="10" src="https://github.com/user-attachments/assets/3b33fae6-1ee1-49a5-aeb0-c8626277d906" />

## Conditional Access Policies

10. I am now going to create several conditional access policies. First, we have a policy name KY-01-Require-MFA-ALL-Users. Adding an extra layer of protection besides just a password.
    
    <img width="2540" height="487" alt="11" src="https://github.com/user-attachments/assets/c6c1d352-7b8a-4268-a869-893aec51daa9" />

11. Next, I have created KY-02-Block-Legacy-Auth. Which prohibits sign-in attempts from older, less secure protocols, preventing attackers from bypassing MFA as legacy protocols cannot prompt for it.
    
    <img width="2557" height="519" alt="12" src="https://github.com/user-attachments/assets/d381ab89-9016-4595-b463-efb563b0c651" />

12. Here we have our third policy named KY-03-Admins-Strong-Auth. Apply stricter rules for high-privilege accounts. The compromise of an admin account is much more damaging than a normal user account, as they can access sensitive data and grant permissions.
    
    <img width="2554" height="549" alt="13" src="https://github.com/user-attachments/assets/5ffe1482-9c8b-49ed-8858-d9a7411cd8d2" />

13. Lastly, we have KY-04-High-Risk_Signins. To protect accounts when suspicious activity is detected, such as sign-ins from unusual locations or devices.
     
    <img width="2559" height="580" alt="14" src="https://github.com/user-attachments/assets/45ccc8bf-032e-4739-8788-d31d3e488dce" />

## Privileged Identity Management (PIM)

14. I have set up Privileged Identity Management (PIM). I use PIM to enforce Just-In-Time (JIT) Access. It ensures least privilege, reduces the risk of permanent high-level access, provides audit trails, and integrates with MFA and Conditional Access for extra security.

    I don't want the Admins to have permanent elevated access, they can activate the access only when needed, which reduces the attack surface

    In this screenshot, I have set up Just-In-Time (JIT) Access with the limitations as:

    - Require MFA
    - Require justification on assignment
    - Activation duration max 4 hours
      
    
    <img width="2559" height="746" alt="15" src="https://github.com/user-attachments/assets/f78bdb09-5d65-4936-88b4-3efdcc69fc70" />


## Project Summary: Identity and Access Management in Azure

This project focuses on building a secure and efficient Identity and Access Management (IAM) system in Microsoft Azure. The goal is to make sure the right people have access to the right resources while keeping sensitive data safe. To achieve this, I have used Azure Active Directory (Azure AD) to manage users and groups, Role-Based Access Control (RBAC) to assign permissions based on roles, and Multi-Factor Authentication (MFA) to add an extra layer of security.

I also implement policies to control access based on conditions like user location or device, and monitor activity for any unusual behavior. Lastly, I have enforced  Privileged Identity Management (PIM) to reduce the risk of permanent high-level access by introducing Just-In-Time (JIT) Access.

I now have a small organization that has a scalable and secure IAM system that protects data, supports smooth collaboration, and makes managing access simple and reliable.






















