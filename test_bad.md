=== SMB Direct
==== windows 10 pro ent
RDMA 가 활성화 되어있는지만 확인 하면 됨.
SMB Direct 패키기를 기본 설치됨.
* 멜라녹스 드라이버 설치
* enable RDMA
Get-NetAdapterRDMA
Enable-NetAdapterRDMA ibs1
==== Ubunto 20.10 desktop
* 멜라녹스 드라이버 설치
* SMB Direct 가 기본적으로 비활성화 되어있으서 CIFS 를 따로 빌드 해야함.
** kernel 소스 받아서 SMB Direct 피쳐를 설정한 후 빌드.
** 빌드된 커널(5.8.18) 로 부팅.
** modprobe cifs
** mount.cifs -o rdma 로 마운트.
그리나 CIFS 를 빌드하려면 여러가지 문제가 발생.
빌드에서 발생하는 모든 문제를 해결 했지만.
마운트가 안되는 문제 발생.
windows의 문제인지 linux 의 문제인지 정확한 확인이 필요한 상황.
* action plan
** case 1: Windows 2019 Server 2대를 설치하여 SMB Direct 동작 확인.
** case 2: Linux Ubunto 20.10 2대를 설치하여 SMB Direct 동작 확인.
case 2는 OS 설치 없이 Live CD로 부팅하여 테스트가 가능 하므로 구성 후 테스트 진행.

=== Ubunto 20.10 live toram - from 2020/10/28 : HPN Infiniband 
* grub boot
e : edit mode
search for the line starting with linux and add the option "toram" right after.
* install modules
apt install opensm librdmacm-dev mstflint ibutils rdma-core
modprobe ib_umad ib_cm ib_ipoib

=== list of MLNX_OFED_LINUX-5.2-* /DEBS
* revHPNetwork_IB_RDMA.xlsx > list_pkgs
ibacm ibverbs-utils mstflint openmpi opensm rdmacm-utils rdma-core
ibdump ibutils2
