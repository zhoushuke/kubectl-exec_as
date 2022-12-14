# kubectl-plugins
A collection of plugins installable via [Krew](https://github.com/GoogleContainerTools/krew)

###### Note
- All coding was written to maintain compatibility across both BSD and GNU.

#### Installing with Krew
```
kubectl krew install exec-as
kubectl krew install prompt
```

#### To Uninstall
```
kubectl krew remove exec-as
```
To remove the prompt plugin:
```
kubectl krew remove prompt
ex '+g/function kubectl()/d' -cwq ~/.bash_profile
ex '+g/KUBECTL_\(.*\)_PROMPT/d' -cwq ~/.bash_profile
```


## kubectl exec-as
![exec](https://user-images.githubusercontent.com/22456127/54227565-97ae8d80-44d6-11e9-907c-8297a8b54010.gif)
- Like kubectl exec, but offers a --user flag to exec as root (or any other user)
- Works by mounting a docker socket as a volume
- You must be in the same namespace as the target pod or you can use ```-n namespace``` option to specify the namespace
- Kudos to mikelorant for thinking of the docker socket! :)

Usage: ```kubectl exec-as [OPTIONS] <pod name> [-- <commands...>]```

Option | Required | Description | Example
------------- | ------------- | ------------- | -------------
-h | N | Show usage | *`kubectl exec-as -h`*
-d | N | Enable debug mode. Print a trace of each commands |  *`kubectl exec-as -d kafka-0`*
-n | N | The namespace scope for this CLI request | *`kubectl exec-as -n infra kafka-0`*
-u | N | User to exec as. Defaults to root | *`kubectl exec-as -u kafka kafka-0`*
-c | N | Specify container within pod | *`kubectl exec-as -c burrow-metrics kafka-0`*
-- | N | Pass an optional command. Defaults to /bin/sh | *`kubectl exec-as kafka -- ls /etc/burrow`*



## kubectl prompt
![prompt](https://user-images.githubusercontent.com/22456127/47271066-91793e00-d542-11e8-9a97-71f2457aef51.gif)
- Displays a warning prompt when issuing commands in a flagged cluster or namespace
- Commands that trigger the prompt include ```create, scale, delete, apply, etc.,```

Start by flagging environments to prompt on:
- Flag a namespace:
```kubectl prompt add -n production```
- Flag a cluster:
```kubectl prompt add -c my-cluster```
- List flagged environments:
```kubectl prompt list```
- Clear flagged environments:
```kubectl prompt remove```
- View description:
```kubectl prompt```
