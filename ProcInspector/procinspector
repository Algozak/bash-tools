#!/bin/bash

if [ ! -d "/proc/$1" ]; then
  echo "Process $1 does not exist"
  exit 1
fi

#process name
name=$(cat /proc/$1/cmdline | tr '\0' ' ')
#process status
status=$(grep "State" /proc/$1/status | awk '{print $2,$3}')
#process memory
mem=$(grep "VmRSS" /proc/$1/status | awk '{print $2,$3}')
#process Open FDs
fds=$(lsof -p $1 | wc -l)
#process Binary inode
inode=$(stat -c "%i" /proc/$1/exe)
#process Binary links
links=$(stat -c "%h" /proc/$1/exe):
#process Cgroup
cgroup=$(cat /proc/$1/cgroup)
#process Namespace PID
ns_pid=$(readlink /proc/$1/ns/pid)
ns_pid=${ns_pid#*[}
ns_pid=${ns_pid%]}
#process NameSpace Network
ns_net=$(readlink /proc/$1/ns/net)
ns_net=${ns_net#*[}
ns_net=${ns_net%]}
#process NameSpace Mount
ns_mnt=$(readlink /proc/$1/ns/mnt)
ns_mnt=${ns_mnt#*[}
ns_mnt=${ns_mnt%]}


show () {
  printf "╔════════════════════════════════════╗\n" 
  printf "║ Process Inspector — PID %-11s║\n" "$1"
  printf "╠════════════════════════════════════╣\n"
  printf "║ Command: %-26s║\n" "$name" 
  printf "║ State: %-28s║\n" "$status" 
  printf "║ Memory: %-27s║\n" "$mem" 
  printf "║ Open FDs: %-25s║\n" "$fds" 
  printf "║                                    ║\n"
  printf "║ Namespaces:                        ║\n"
  printf "║ PID: %-30s║\n" "$ns_pid" 
  printf "║ NET: %-30s║\n" "$ns_net" 
  printf "║ MNT: %-30s║\n" "$ns_mnt" 
  printf "║                                    ║\n"
  printf "║ Cgroup: %-27s║\n" "${cgroup#*::}" 
  printf "║                                    ║\n"
  printf "║ Binary inode: %-21s║\n" "$inode" 
  printf "║ Binary links: %-21s║\n" "$links" 
  printf "╚════════════════════════════════════╝\n"
}


show "$1"

