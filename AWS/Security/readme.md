# Security

1. Encryption
    1. Encryption in flight is done through using SSL certificate
        1. Ensures MITM (Man in the middle) attack cannot happen
    2. Server side encryption at rest
        1. Data is encrypted after being received by the server
        2. Data is decrypted before being sent
        3. The encryption/decryption keys are managed using some management service
    3. Client side encryption
        1. Data is encrypted by client and never decrypted by the server
        2. Data will be decrypted by a receiving client
        3. Could leverage envelope encryption
2. KMS
    1. Key management service
    2. AWS KMS manages keys for us
    3. Integrated with IAM for authorisation
    4. Can be used by SDK and CLI
    5. Customer Master Key (CMK)
        1. Symmetric (AES-256 keys)
            1. Single encryption key that is used to encrypt and decrypt
            2. Necessary for envelope encryption
            3. AWS services that are integrated with KMS use symmetric CMKs
            4. You never get access to the key unencrypted
                1. Must call KMS API to use
        2. Asymmetric (RSA & ECC key pairs)
            1. Public  key for encryption
            2. Private key for decryption
            3. Used for sign/verify options
            4. The public key is downloadable
            5. Cannot access the private key unencrypted
            6. Use
                1. Encryption outside of AWS
        3. Types
            1. AWS managed service default CMK - free
            2. User keys created in KMS
            3. User keys imported (must be 256 bit symmetric keys)
    6. KMS gives ability to fully manage keys & policies
        1. Create
        2. Rotation policies
        3. Diable
        4. Enable
    7. Using Cloudtrail we can audit key usage
    8. Use
        1. To share sensitive information
    9. Benefit of KMS is that CMK cannot be retrieved by the user and CMK can be rotated for extra security
    10. Encrypted secrets can be stored in code/environment variables but not in plaint text
    11. KMS can only help in encrypting upto 4KB of data per call
        1. If data > 4KB, use envelope encryption
    12. To give access to KMS
        1. Make sure the key policy allows the user
        2. Make sure the IAM policy allows the API calls
    13. KMS keys are bound to specific region
    14. KMS key policies
        1. They are resource policies
        2. You cannot control access without them
        3. Default policy
            1. Created if you don’t provide a specific KMS key policy
            2. Complete access to the key to the root user - entire AWS account
            3. Give access to the IAM policy to the key
        4. Customer KMS key policy
            1. Define users, roles that can access the KMS key
            2. Define who can administer the key
            3. Useful for cross-account access of your KMS key
    15. Copy snapshot across accounts
        1. Create a snapshot that is encrypted with your own CMK
        2. Attach a KMS key policy to authorise cross-account access
        3. Share the encrypted snapshot
        4. In the target create a copy of snapshots encrypt it with KMS key in account
        5. Create a volume from the snapshot
    16. KMS key rotation
        1. Automatic rotation
            1. For customer managed CMK
                1. If enabled: automatic key rotation happens every 1 year
                2. Previous key is kept active to decrypt old data
                3. New key has same CMK ID only the backing key is changed
            2. Cannot rotate AWS managed CMK
        2. For manual key rotation
            1. When you want to rotate key according to your time period eg 90 days
            2. New key created has different CMK ID
            3. You should keep the previous key active to decrypt old data
            4. It is better to use alias to hide the change of key for the application
                1. Update Alias to hide the change of key application 
