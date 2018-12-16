# k8s-webhook

1. `cd docker`
2. `docker build . -t localserver`
3. Cut and Paste the root CA from the docker build output `Step 12/13 : RUN cat rootCA.crt | base64 | tr -d '\n'` and replace the value currently in https://github.com/rwibawa/k8s-webhook/blob/master/k8s/hook.yaml#L14
4. `cd ../k8s`
5. `kubectl create -f deployment.yaml`
6. `kubectl create -f service.yaml`
7. `kubectl create -f hook.yaml`
8. `kubectl create -f test.yaml`

## Output:
```bash
$ kubectl create -f hook.yaml
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook created
$ kubectl get mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook
NAME      CREATED AT
webhook   2018-12-16T01:03:19Z
$ kubectl describe mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook
Name:         webhook
Namespace:
Labels:       <none>
Annotations:  <none>
API Version:  admissionregistration.k8s.io/v1beta1
Kind:         MutatingWebhookConfiguration
Metadata:
  Creation Timestamp:  2018-12-16T01:03:19Z
  Generation:          1
  Resource Version:    566857
  Self Link:           /apis/admissionregistration.k8s.io/v1beta1/mutatingwebhookconfigurations/webhook
  UID:                 60cc0b77-00ce-11e9-af98-08d0f8f11711
Webhooks:
  Client Config:
    Ca Bundle:  LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUdEakNDQS9hZ0F3SUJBZ0lKQU9zTGpOaFJ6VU9wTUEwR0NTcUdTSWIzRFFFQkN3VUFNSUdiTVFzd0NRWUQKVlFRR0V3SlZVekVUTUJFR0ExVUVDQXdLVG1WM0lFcGxjbk5sZVRFVE1CRUdBMVVFQnd3S1VISnBibU5sZEc5dQpJREVTTUJBR0ExVUVDZ3dKUkc5M0lFcHZibVZ6TVF3d0NnWURWUVFMREFOUVNVSXhGakFVQmdOVkJBTU1EU291ClpHVm1ZWFZzZEM1emRtTXhLREFtQmdrcWhraUc5dzBCQ1FFV0dYTmpiM1IwTG5KaGFHNWxja0JrYjNkcWIyNWwKY3k1amIyMHdIaGNOTVRneE1qRTFNak0wTlRNeldoY05NakV4TURBME1qTTBOVE16V2pDQm16RUxNQWtHQTFVRQpCaE1DVlZNeEV6QVJCZ05WQkFnTUNrNWxkeUJLWlhKelpYa3hFekFSQmdOVkJBY01DbEJ5YVc1alpYUnZiaUF4CkVqQVFCZ05WQkFvTUNVUnZkeUJLYjI1bGN6RU1NQW9HQTFVRUN3d0RVRWxDTVJZd0ZBWURWUVFEREEwcUxtUmwKWm1GMWJIUXVjM1pqTVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx6WTI5MGRDNXlZV2h1WlhKQVpHOTNhbTl1WlhNdQpZMjl0TUlJQ0lqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FnOEFNSUlDQ2dLQ0FnRUF2bkIyZnA4eHo4VVNKaEJUCkhtZy8wbWQ4TG9rOWM5NTlHTjkyYkRqSnc5enhCRUV6Q0t0U3ZKYVA0S09HaWRJc0R0aVRqdXhlSjh5U2VYQ2gKWGllSWJqNnpYRVZBVmNTdU1oakh2ZjhvWi96YkIxR2NIZEtLYmloRHAva0hLc2FLTUY2aERlblMrOWljU2hYeQp1Ry9OVzdFbGJzL2JLVC84VytaSCtWK3RXWHBrNG9aK2xPR0FvcVQ5bXhYZW5DWWNFSFRvYjBJVi9NTUNmQXdrCkpaOC9WV3lLekhCTmdQZW5zZDlXRHB1VkF6Uy9LSlhSeHFaMFRFOUJOc2Y1bWs0NTdzNk41SXBKKzExZjZrTlUKTVB3T082Y0RiTUdmWkFsd0ZwaWw3c0tOSlFMZXM1U3AvNUpxZWdGN1Ewb3k5WHVUNzRtM2VuVDVlbG93eUxnZwpsYm1ZWmxKTnVQeFQ5cjZLWDdzQlJNRkxWMzdqeTQ1NDNkZWpvRlNoRjhjL0JiNW9Mb1JobkEwTlZuOWljZ0krCldqaWRYRTZWeVh3RTQ2cDNPcy9GV2xRNGRKNWx2eUl0ajJFNkdhdEVUZkxsb3MyeWdDK084MVNKOEdOSENTYjQKUExlZEVhNllFL041TW5rNkZrSVprK3cxUzVoK1VvSEJEblFVM0VGTnRoU01sR0NzN2svS1VnVlhZQzQzeC9wbgppTzJucEVVOVBKQXBIa0p6SmE5Q1lQRGhlZ1AxMlA5Vlg3K0JKTmw1dnZ2UEFYdkJ0U3p0bVNXMU9MRmMzZ0k5CjlDaHU3MmFRWU5za2M3N2NvUkZOTFMzZnhlbGRhb0pyZnFpTEZ6VmhGcEZObDZIT0ZzMVc2WkhKWSsybm5RMDAKQUptbmR0YmcwZXdOZGRzWWgzTGl1YzdaZXo4Q0F3RUFBYU5UTUZFd0hRWURWUjBPQkJZRUZMSnFuU0IyVW4wegptMkp2M0tyRDZ6R0xQbExkTUI4R0ExVWRJd1FZTUJhQUZMSnFuU0IyVW4wem0ySnYzS3JENnpHTFBsTGRNQThHCkExVWRFd0VCL3dRRk1BTUJBZjh3RFFZSktvWklodmNOQVFFTEJRQURnZ0lCQUs0MFp1OWYvaVBCdDlYWjhZQ2QKbnJPWE5KUndPNzZNajRRWE4zSWJxZ1UzM2FXMHQydlVaUUNwSzl6NkExOXJPNkcyVGVLQ3ZTNHNMc09jcTJITwpqVTgwa3JvMW1pTFFBQnRjWk1wajFLUi9Zd2FIM1NSTnYwQ1VtZDZDRTZidWltelB6Z1MzUkJwMzBlcnU2QXU2CnZ0TElKR3V3V29lQmhUVWVycDFUVlJKcEtjRVIxdFZGK1J2MkN2Vng3eGc1VEJIV2NXeDFTWUFwN3dzUWVhbGwKUHhKaENWR0RhaCsrTVpCa2toc0dDaW9jWXk2cU9TTUZTeXhFYWRIM1lNblB4Qm1nMDkvT2Y5Rk00endIWlF2TQpEMDRYU3Z2bUdqSGpYTjZpTzlSQmtqZGVlNzZHeUV5SHhodkQ3WjZ5SEc4YmpleFFLNjFvSWJtMTZTOUxaV3RNCmFRQzFvSTlFNXU1QjJ6WS9QL2g0WjFsQTlqQ0s3Q3JBb3V3Q2lxNU53R1RCOEYvQlFqWml2OGFqcCsreXNhdUEKTHNMZStONGoxUzVMWnoranNWN0l1SUo3QUVxdVFoYmllUy9NdWYzalJjbVR2YkFua2Q5OWw5WEZCRkY2Qlc0Nwpzb21reEQrbURjNjI4VzVRbytTZ0dJb3lZUEVNSlBFeE5QNUVneDVZajhmRGZ6QUUzdlA1Q2IwOW1maEhqNy95CkZPUHNNWUJYb1ZaYXdiYWYwYmVqNjNUY1hLdkFkVWR4V0Q2Q2RBSTY2NFkvQjUzT3llNzdMeTQvTEx6U3dzLzgKQnNtTENDQ3RMRUtpU01mOVRISmIzZXVFTDY1eFc0UEFaQzJNZCtadkxmMmdDdTR0QmFONDlMOWl0RkpVR2lQTApXVUdiRlV5dWFkaWRKSFhXano0WWU4VzUKLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    Service:
      Name:        webhook-service
      Namespace:   default
      Path:        /mutate
  Failure Policy:  Fail
  Name:            webhook-service.default.svc
  Namespace Selector:
  Rules:
    API Groups:

    API Versions:
      v1
    Operations:
      CREATE
    Resources:
      pods
Events:  <none>

$ kubectl create -f test.yaml
deployment.apps/test created
$ kubectl get pods
NAME                              READY     STATUS    RESTARTS   AGE
k8s-demo-85f8fd799-lwzcx          1/1       Running   0          3d
private-reg                       1/1       Running   0          5d
test-6f79f9f8bd-w4d7d             1/1       Running   0          24s
webhook-server-57f8b87c95-tdm9x   1/1       Running   0          1h
wordpress-7bdfd5557c-8cdgb        1/1       Running   0          5d
wordpress-mysql-bcc89f687-rgs6h   1/1       Running   0          5d
$ kubectl describe pod test
Name:           test-6f79f9f8bd-w4d7d
Namespace:      default
Node:           minikube/192.168.122.157
Start Time:     Sat, 15 Dec 2018 17:04:16 -0800
Labels:         component=test
                foo=bar
                pod-template-hash=2935959468
Annotations:    <none>
Status:         Running
IP:             172.17.0.11
Controlled By:  ReplicaSet/test-6f79f9f8bd
Containers:
  test:
    Container ID:  docker://bb9fd6e6ecb94d4d5f9756a04c848a21f44cb6e2f4c06b58bd0daefaf15e905a
    Image:         node:8
    Image ID:      docker-pullable://node@sha256:dd2381fe1f68df03a058094097886cd96b24a47724ff5a588b90921f13e875b7
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/sh
      -c
      --
    Args:
      while true; do sleep 30; done;
    State:          Running
      Started:      Sat, 15 Dec 2018 17:04:20 -0800
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-nksb4 (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-nksb4:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-nksb4
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              1m    default-scheduler  Successfully assigned test-6f79f9f8bd-w4d7d to minikube
  Normal  SuccessfulMountVolume  1m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-nksb4"
  Normal  Pulled                 1m    kubelet, minikube  Container image "node:8" already present on machine
  Normal  Created                1m    kubelet, minikube  Created container
  Normal  Started                1m    kubelet, minikube  Started container
```
