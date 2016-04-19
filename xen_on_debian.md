1. ׼��LVM��
���������
```
  apt-get install lvm2
  pvcreate /dev/sda4  # �ڷ����Ͻ���PV
  vgcreate vg0 /dev/sda4 # ������Ϊvg0�ľ���
  lvcreate -n centos7 -L 20G vg0 # ������Ϊcentos7�ľ�
```

2. ��װXen
���������
```
  apt-get install xen-linux-system
```
3. ׼������
�����У�ʹ��Linux Bridge���������������ӿ�
���������װ���ߣ�
```
  apt-get install bridge-utils
```
��```/etc/network/interfaces```�ļ��У�����ϵͳ���磺
```
auto eth0
iface eth0 inet manual

auto xenbr0
iface xenbr0 inet static
  bridge_ports eth0
  address 192.168.1.148
  netmask 255.255.255.0
  gateway 192.168.1.1	
```

4. ����������������ļ�
  ������������ļ�����Ϊcentos7.cfg���������£�
```
kernel = "/usr/lib/xen-4.4/boot/hvmloader"
builder = 'hvm'
memory = 4096
vcpus = 4
name = "centos7"
vif = ['type=vif,bridge=xenbr0']
disk = ['phy:/dev/vg0/centos7,hda,w','file:/root/Downloads/centos7.iso,hdc:cdrom,r']
acpi = 1
device_model_version = 'qemu-xen'
boot = "d"
sdl = 0
vnc = 1
serial = 'pty'
vnc = 1
vncdisplay = 1
vnclisten = ""
vncpasswd = ""
```

5. ���������
���������
```
  xl create centos7.cfg
  xvnc4viewer 192.168.1.148:5901   # port�� vncdisplay ����
```
