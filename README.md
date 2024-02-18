# Create two Namespaces and connect them using veth VM


Create two namespaces
```
ip netns add ns1
ip netns add ns2
```
Create veth pair
```
ip link add veth0 type veth peer name veth1
```
Move one end of the veth pair to ns1 and the other end to ns2
```
ip link set veth0 netns ns1
ip link set veth1 netns ns2
```
Configure IP addresses inside the namespaces
```
ip netns exec ns1 ip addr add 10.0.0.1/24 dev veth0
ip netns exec ns2 ip addr add 10.0.0.2/24 dev veth1
```
Bring up the interfaces inside the namespaces
```
ip netns exec ns1 ip link set veth0 up
ip netns exec ns2 ip link set veth1 up
```
