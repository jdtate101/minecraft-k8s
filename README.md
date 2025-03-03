# Instructions

You Simply need to create a namespace on the k8s server:

```
kubectl create ns minecraft-1
```

You will need to download and modify the manifest to input your Minecraft userID in the OPS and WHITELIST sections...

Then deploy the manifest into the namespace. A separate namespace can be created per demo station. The external loadbalancer should take care of the random external port assignment:

```
kubectl apply -f manifest.yaml -n minecraft-1
```

You should now have a single 10Gbi PVC for the persistent world, a deployment managing the server and an external exposure via load balancer.

You can access the world via the Minecraft java client and point it to the loadbalancer IP and port address. 

The world is a new install, randomly generated world without the "explosive" demo, so create a location profile with the following details in Kasten:

```
Endpoint: https://s3.kodu.uk
Access Key: (ask James)
Secret Key: (ask James)
Region: custom-other
Bucket: demo
```

Create an import policy on demand and ask James for the `import-string` pointing at the S3 bucket.

Run the import policy and then restore the imported application and do a `data only restore`

Once the deployment is scaled back up, you can access the world and should be standing upon a platform with a stairway in front of you leading up to another platform looking at a large VEEAM logo. The is a switch, if you right click on the switch (may take two presses) it will activate the dynamite and blow up the logo.

I would recommend creating a local backup policy and pushing to an AWS/Azure bucket before you run the demo.

# Recovery

Simply issue a data only restore to rollback the explosion and restore the logo.
