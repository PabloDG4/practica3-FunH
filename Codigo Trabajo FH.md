sudo fdisk -l
sudo fdisk /dev/sdb
o               
n               
p               
1               
                
+20G           
n               
p               
2
                
+10G           
n               
p
3
                
+15G            
n               
e
4
                
n              
               
+10G            
n             
                
+15G            
t              
1              
83              
t
2
83
t
3
83
t
5               
83
t
6              
83
p             
w             
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.ext4 /dev/sdb2
sudo mkfs.ext4 /dev/sdb3
sudo mkfs.ext4 /dev/sdb5  
sudo mkfs.ext4 /dev/sdb6
sudo mount /dev/sdb1 /media/sdb1
echo "Soy la partición 1 MBR y tengo un tamaño de 20GiB" | sudo tee /media/sdb1/particion1.txt
sudo umount /media/sdb1

sudo mount /dev/sdb2 /media/sdb2
echo "Soy la partición 2 MBR y tengo un tamaño de 10GiB" | sudo tee /media/sdb2/particion2.txt
sudo umount /media/sdb2

sudo mount /dev/sdb3 /media/sdb3
echo "Soy la partición 3 MBR y tengo un tamaño de 15GiB" | sudo tee /media/sdb3/particion3.txt
sudo umount /media/sdb3

sudo mount /dev/sdb5 /media/sdb5
echo "Soy la partición 5 MBR (lógica) y tengo un tamaño de 10GiB" | sudo tee /media/sdb5/particion5.txt
sudo umount /media/sdb5

sudo mount /dev/sdb6 /media/sdb6
echo "Soy la partición 6 MBR (lógica) y tengo un tamaño de 15GiB" | sudo tee /media/sdb6/particion6.txt
sudo umount /media/sdb6
sudo nano /etc/fstab
#Dentro de sudo nano
/dev/sdb1  /media/sdb1  ext4  defaults  0  2
/dev/sdb2  /media/sdb2  ext4  defaults  0  2
/dev/sdb3  /media/sdb3  ext4  defaults  0  2
/dev/sdb5  /media/sdb5  ext4  defaults  0  2
/dev/sdb6  /media/sdb6  ext4  defaults  0  2
sudo fdisk -l
sudo gdisk /dev/sdc
o               
y              
n               
                
+20G            
8300            
n               
                
+15G            
8300            
p               
w               
y               
sudo mkfs.ext4 /dev/sdc1
sudo mkfs.ext4 /dev/sdc2
sudo mkdir -p /media/sdc{1,2}

sudo mount /dev/sdc1 /media/sdc1
echo "Soy la partición 1 GPT y tengo un tamaño de 20GiB" | sudo tee /media/sdc1/particion1.txt
sudo umount /media/sdc1

sudo mount /dev/sdc2 /media/sdc2
echo "Soy la partición 2 GPT y tengo un tamaño de 15GiB" | sudo tee /media/sdc2/particion2.txt
sudo umount /media/sdc2
sudo nano /etc/fstab
#Dentro de sudo nano
/dev/sdc1  /media/sdc1  ext4  defaults  0  2
/dev/sdc2  /media/sdc2  ext4  defaults  0  2
sudo mount -a  # Monta todo según fstab
ls -l /media/sdb* /media/sdc*  # Deberías ver los archivos .txt