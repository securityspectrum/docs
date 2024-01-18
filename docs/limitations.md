# Limitations

In this section, we describe the current limitations in our SIEM platform.

## Encryption

We do not support the following functionalities:

* **MAC address** encryption.
* **Key rotation** on a recurrent time basis (e.g. day, week, or month).
* **Multi-user** encryption support - where each user has its own decryption keys.
* **RBAC** based on fields.

## Log-shipper agents
* **fluent-bit** is not supported on Windows for two reasons:
   - **kafka** *output* plugin is disabled on Windows by fluent-bit organization, see [#1944](https://github.com/fluent/fluent-bit/issues/1944).
   - **encrypt** *filter* a plugin developed by our organization is not fully implemented to support Windows OS.