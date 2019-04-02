# CLI based instructions for installing and running the Palo Alto Networks Security Adapter for Istio 

## Quick install with Google Marketplace 

Get up and running with a few clicks! Install the Palo Alto Networks Service Mesh Security adapter 
to your kubernetes Engine cluster using Google Cloud Marketplace. 
Follow the on-screen instructions: TODO: link to solution details page 


## Command line instructions  

Follow these instructions to install Palo Alto Networks Service Mesh Security Adapter from the command line. 

### Prerequisites

- Setup kubernetes cluster 
- Setup Istio 
- Validate Istio 

    - Ensure that Istio and all its components have been successfully installed. 
    - Execute: ```kubectl get po -n istio-system```

      The output should resemble: 
      ```
	   vinay@vv15-ubuntu18:~/go/src/$ kubectl get po -n istio-system
		   NAME                                      READY   STATUS      RESTARTS   AGE
		   grafana-9cfc9d4c9-dqp9f                   1/1     Running     0          20d
		   istio-citadel-74df865579-9qd2s            1/1     Running     0          20d
		   istio-cleanup-secrets-mjlhq               0/1     Completed   0          20d
		   istio-egressgateway-96fb7964f-jdn6x       1/1     Running     0          20d
		   istio-galley-8487989b9b-zhclr             1/1     Running     0          20d
		   istio-grafana-post-install-2p6hw          0/1     Completed   0          20d
		   istio-ingressgateway-75d6486b96-q762r     1/1     Running     0          20d
		   istio-pilot-78776dd4bd-tkpsn              2/2     Running     0          20d
		   istio-policy-67f87dd-zjnvp                2/2     Running     0          20d
		   istio-security-post-install-j9wzc         0/1     Completed   0          20d
		   istio-sidecar-injector-5cfcf6dd86-7bfd6   1/1     Running     0          20d
		   istio-telemetry-9b566b9c7-c9phj           2/2     Running     0          20d
		   istio-tracing-ff94688bb-5thvh             1/1     Running     0          20d
		   prometheus-f556886b8-754zr                1/1     Running     0          20d
		   servicegraph-55d57f69f5-k7vt2             1/1     Running     0          20d
      ```

- Install the application resource 

  TODO: provide details on how to install the Application CRD

- Install the Palo Alto Networks Security Policy Simulator Service 

  TODO: provide details on installation 

### Commands 

Set environment variables (modify to match your environment): 

```
export APP_PARAMETERS='{"name": "pansecurityadapter", "namespace": "istio-system", "appName": "pansecurityadapter", "securityPolicyApiEndpoint": "10.28.3.59", "securityPolicyApiPort":"9080", "securityAdapterImageName": "gcr.io/redlock-gcp/pan-servicemesh-security:2.3"}'
```

Expand manifest template:

```
cat manifest/* | envsubst > expanded.yaml
```

Run kubectl:

``` kubectl apply -f expanded.yaml ```

### Verify the installation of the Palo Alto Networks Adapter 


   The output should resemble: 
   ``` 
	vinay@vv15-ubuntu18:~/go/src/$ kubectl get po -n istio-system
		NAME                                      READY   STATUS      RESTARTS   AGE
		grafana-9cfc9d4c9-dqp9f                   1/1     Running     0          20d
		istio-citadel-74df865579-9qd2s            1/1     Running     0          20d
		istio-cleanup-secrets-mjlhq               0/1     Completed   0          20d
		istio-egressgateway-96fb7964f-jdn6x       1/1     Running     0          20d
		istio-galley-8487989b9b-zhclr             1/1     Running     0          20d
		istio-grafana-post-install-2p6hw          0/1     Completed   0          20d
		istio-ingressgateway-75d6486b96-q762r     1/1     Running     0          20d
		istio-pilot-78776dd4bd-tkpsn              2/2     Running     0          20d
		istio-policy-67f87dd-zjnvp                2/2     Running     0          20d
		istio-security-post-install-j9wzc         0/1     Completed   0          20d
		istio-sidecar-injector-5cfcf6dd86-7bfd6   1/1     Running     0          20d
		istio-telemetry-9b566b9c7-c9phj           2/2     Running     0          20d
		istio-tracing-ff94688bb-5thvh             1/1     Running     0          20d
		pansecurityadapter-6789d7d88f-49tmk       1/1     Running     0          24s
		prometheus-f556886b8-754zr                1/1     Running     0          20d
		servicegraph-55d57f69f5-k7vt2             1/1     Running     0          20d
``` 

You will see the Palo Alto Networks security adapter's container. In this case it is: 
`pansecurityadapter-6789d7d88f-49tmk`


## Install an application onto the Kubernetes cluster 

`Script link`: ``` https://github.com/vinayvenkat/gke_k8s_deployer/blob/master/manage_app.sh ```

Details on how to setup the export variables to be able to access the cluster are also 
provided in the script shown above. 

## Run some traffic to any applications deployed on your cluster


## View the logs on the Stackdriver Console on GCP

- Login to the GCP console
- Navigate to Stackdriver logging tab on the left 
- Filter to the following logs: `GKE Container -> <cluster name> -> istio-system (namespace)` 

You should be able to see the logs pertaining to intercontainer traffic on your kubernetes cluster
running with the Istio Service Mesh.  


