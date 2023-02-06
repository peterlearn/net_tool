# 获取回环ip
````
package main

import (
	"fmt"
	"net"
)

func main() {
	ip := getLoopbackAddress(true)
	fmt.Println(ip)
}

func getLoopbackAddress(wantIPv6 bool) string {
	addrs, err := net.InterfaceAddrs()
	if err == nil {
		for _, address := range addrs {
			if ipnet, ok := address.(*net.IPNet); ok && ipnet.IP.IsLoopback() && wantIPv6 == IsIPv6(ipnet.IP) {
				return ipnet.IP.String()
			}
		}
	}
	return "localhost"
}

// IsIPv6 returns if netIP is IPv6.
func IsIPv6(netIP net.IP) bool {
	return netIP != nil && netIP.To4() == nil
}

// IsIPv4 returns if netIP is IPv4.
func IsIPv4(netIP net.IP) bool {
	return netIP != nil && netIP.To4() != nil
}
````
