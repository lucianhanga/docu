# Identity Management

Identity solution management include the ability to both identify users as well as validate permissions:

- **Authentication**
  - identify who is attempting to access a resource
  - compares user credentials with the stored credentials in the database
  - required to determine what access rights the user has

- **Authorization**
  - determines what access rights of an authenticated user has
  - requires authentication to be performed first


### Azure Active Directory

**Azure Active Directory (Azure AD) or AAD** is a cloud-based identity and access management service that provides single sign-on and multi-factor authentication to help protect your users from 99.9% of cyber attacks.

- **Azure AD** is a **multi-tenant** service that is **hosted** in the **Microsoft cloud**.
- user accounts created in the tenant are stored in the AAD database.
- users authenticate to AAD using their credentials in order to access resources in the Microsoft cloud.
- Its distinct from the on-premises **Active Directory** service that is used to manage user accounts for on-premises resources. But can be integrated with on-premises AD.

**Azure AD connect** is a tool that can be used to synchronize on-premises AD with Azure AD. The AAD will federate with the on-premises AD. **DirSync** is a tool that can be used to synchronize on-premises AD with Azure AD.

### Multi-Factor Authentication (MFA)

**Multi-Factor Authentication (MFA)** is a method of **authentication** that requires more than one **factor** to verify the identity of a user.

### Policy Management

**Policy Management** is the process of creating and managing **policies** that define the **rules** that are used to control access to resources.
Its missing from AAD in comparison to AD DS on-premises.
