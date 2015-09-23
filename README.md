#Summary

The example-nozzle-release is written to be a starting point for nozzle authors to learn how to build and deploy a nozzle.

#Prerequisites

- BOSH CLI
- A working Cloud Foundry environment. This release is setup to work with a CF BOSH lite environment, but you should be able to deploy it to any environment.
- Add example-nozzle UAA client in Cloud Foundry deployment manifest
```
properties:
  uaa:
    clients:
      example-nozzle:
        access-token-validity: 1209600
        authorized-grant-types: authorization_code,client_credentials,refresh_token
        override: true
        secret: example-nozzle
        scope: openid,oauth.approvals,doppler.firehose
        authorities: oauth.login,doppler.firehose
```
- bosh deploy your Cloud Foundry environment again with the above changes present

#Deploying

```
scripts/make_manifest_spiff_bosh_lite
bosh create release
bosh upload release
bosh deploy
```

#Viewing

The example-nozzle simple outputs all the data coming from the firehose to its log files. To view its output, you can SSH into the example-nozzle box and look at the logs

```
bosh ssh example-nozzle
cd /var/vcap/sys/log/example-nozzle
tail -f *.log
```


