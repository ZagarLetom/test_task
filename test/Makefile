
FLAGS := -Wall -Wextra -Wstrict-prototypes -Wmissing-declarations -Wdeclaration-after-statement -Werror
INSTALL := sudo apt-get install -y
DPDK_version := 23.11.2
LINK := https://fast.dpdk.org/rel/dpdk-23.11.2.tar.xz

all:
	$(INSTALL) wget tar
	wget $(LINK)
	tar xf dpdk-$(DPDK_version).tar.xz
	cd dpdk-$(DPDK_version)
	meson build
	ninja -C build
	meson -Dexamples=all build
	mkdir -p /dev/hugepages
	mountpoint -q /dev/hugepages || mount -t hugetlbfs nodev /dev/hugepages
	echo 64 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages

run:
	./test

clean:
	rm -rf dpdk*

format:
	clang-format -i *.h *.c -style=Google
