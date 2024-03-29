# How to use

We describe the steps on how to use our SIEM platform. We describe how to start using the application in a few steps.

## Requirements
* Have an account on securityspectrum.io.
* Must have fluent-bit (log-shipper) with `encrypt` filter plugin and `kafka` output installed on the device which parses and encrypt logs.
   * Get the fluent-bit with `encrypt` plugin from [https://github.com/securityspectrum/fluent-bit/releases](https://github.com/securityspectrum/fluent-bit/releases)
   * Please note that Windows OS is not supported at the moment.
   * The following Operating Systems are supported:
     * ubuntu
     * centos
     * amazonlinux
     * debian
     * raspbian
* Must have at least one of the supported security agents installed that will monitor and generate the logs in JSON. At the current moment, we only support:
   * [x] Zeek
   * [ ] OSSEC
   * [ ] OpenVAS
   * [ ] Suricata


## Quickstart

In this section, we describe how to start receiving event logs generated by `Zeek` and shipped with `fluent-bit` with encrypted PIIs.

### 1. Generate encryption keys and configuration file for fluent-bit
1. Create an account on securityspectrum.io
2. Login and create a first organization. Mark that organization as default.
3. Go to `Settings` -> `Application Settings` -> `Setup Encryption Key` and Click on `Setup encryption key` button to generate encryption keys.
4. Verify and review selected `PII fields` with the `encryption mechanisms` by accessing `Privacy` view.

### 2. Installing and configuring Zeek
1. Install [Zeek](https://docs.zeek.org/en/master/install.html)
2. Stop Zeek with `zeekctl stop`
3. Go to `/opt/zeek/share/zeek/site/local.zeek` and append the following configuration at the end of the file:

        # @load packages
        # Output to JSON format
        load policy/tuning/json-logs.zeek

4. Restart Zeek:

        
        zeekctl deploy
        
5. Verify that the logs are generated in JSON format:


        tail -f /opt/zeek/logs/current/conn.log


### 3. Installing and configuring fluent-bit

1. Install fluent-bit with `encrypt` filter plugin available from here: [https://github.com/securityspectrum/fluent-bit/releases](https://github.com/securityspectrum/fluent-bit/releases)
   * After installation, verify that fluent-bit binary works as expected with `encrypt` plugin with the following command:

       ```fluent-bit -v ...```

2. Create a file `fluent-bit-parsers.conf` with the following contents:
  
      
       [PARSER]
       Name        json-parser
       Format      json
      
3. From the view `Settings` -> `Application settings` -> `Log Shippers`.
   1. If there is no fluent-bit configuration present in the view, click on `Add Token` button on top right to generate new.
   2. Create a new configuration file `fluent-bit.conf` with the generated fluent-bit configuration sample. You can click on the middle icon `Copy configuration` ![Copy configuration](images/copy.png).
   3. Click on the icon `Download certificates`![Download certificates](images/download.png) and extract the three files from it. Make sure that they match the following path:

           rdkafka.ssl.ca.location          /opt/log-shippers/fluent-bit/.certs/kafka-client-cacert.crt
           rdkafka.ssl.certificate.location /opt/log-shippers/fluent-bit/.certs/kafka-client.crt
           rdkafka.ssl.key.location         /opt/log-shippers/fluent-bit/.certs/kafka-client.key

8. Make sure to update the attribute `Master_Enc_Key` value in `fluent-bit.conf` with the `Master Key` value which was generated in the 3rd step.

9. Test fluent-bit with `fluent-bit -c fluent-bit.conf`
