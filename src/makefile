# sudo aptitude install sshpass 
# also: https://wiki.analog.com/university/tools/pluto/users/customizing#enabling_persistent_ssh_keys

#CROSS=/home/user/devel/m2k-fw/buildroot/output/host/bin/arm-linux-gnueabihf-
CROSS=/opt/Xilinx/SDK/2019.1/gnu/aarch32/lin/gcc-arm-linux-gnueabi/bin/arm-linux-gnueabihf-

# default credentials for m2k
target=192.168.3.1
user=root
passwd=analog

%.o: %.cpp
	$(CROSS)g++ -c $< -o $@

main: main.o
	$(CROSS)g++ main.o -o main

clean:
	rm -f *.o main


transfer: main
	sshpass -p "$(passwd)" scp main $(user)@$(target):/root

exec: 
	sshpass -p "$(passwd)" ssh $(user)@$(target) /root/main

run: transfer exec
