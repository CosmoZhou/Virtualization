# Virtualization

Get host type

grep '' /sys/hypervisor/type > /dev/null
rc=$?
if [ $rc -eq 0 ]; then  # Xen Srever/VM
  dmesg | grep -i 'Xen virtual' >/dev/null
  rc=$?
  if [ $rc -eq 0 ];then # Xen VM
    echo "vm"
  else
    echo "ovs"
  fi
else  # Not Xen Server
  dmesg | grep -iE 'KVM|Xen|Vmware|Virtualbox' >/dev/null
  rc=$?
  if [ $rc -eq 0 ];then
    echo "vm"
  else
    echo "physical"
  fi
fi
