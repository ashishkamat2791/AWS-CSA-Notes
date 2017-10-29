# CloudHSM

![Alt_Text](https://blog.gemalto.com/wp-content/uploads/2013/03/aws-cloudhsm-300x242.png "Cloud HSM")
* HSM (Hardware Secuirty Model) is a dedicated physical machine/appliance isolated in order to store security keys and other types of encryption keys used within an application
* The key is used within the domain of the HSM appliance instead of being exposed outside the appliance.

* HSM Appliances have special securiy mechansims to make them more secure:
    * The Security key is only used within the HSM.
    * An HSM client is used to expose the APIs of the HSM.
    * So an application can communicate with HSM to do the encryption (or decryption) of the data that we are requesting.
    * They appliance is physically isolated from other resources.
    * Tamper resistant (build to notify via advanced logging)
    * on AWS, even though they are hosting the appliance, AWS engineers have NO access to the keys (only to manage and upadate the appliance)
    * If the keys are lost or reset (to access the appliance), you will never be able to access the data stored on tne appliance.

    * Some types of keys taht might be stored on HSMs:
        * Keys used to encrypt file systems
        * Keys used to encrypt databases.
        * Keys used to provide DRM
        * Used with S3 encyption

    * When to use CloudHSM instead of something like KMS?

        * Generally, compliance requirements require it or internal security policy require it.
        * Not even AWS engineers have access to the keys on the CloudHSM appliance, only accesss to "manage" the appliance.

