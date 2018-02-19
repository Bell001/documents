# Install OpenMPI

## installation
```
wget https://www.open-mpi.org/software/ompi/v3.0/downloads/openmpi-3.0.0.tar.gz
tar -xvf openmpi-*
cd openmpi-*
./configure --prefix="/usr/local/share/.openmpi"
make
sudo make install
```

## Set PATH  
ไปแก้ที่ /etc/bashrc ให้เป็น global
```
export PATH="$PATH:/usr/local/share/.openmpi/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/share/.openmpi/lib/"
echo export PATH="$PATH:/usr/local/share/.openmpi/bin" >> ~/.bashrc
echo export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/share/.openmpi/lib/" >> ~/.bashrc
echo export PATH="$PATH:/usr/local/share/.openmpi/bin" >> /etc/bashrc
echo export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/share/.openmpi/lib/" >> /etc/bashrc

```

*** ถ้าตอนแก้ไม่ได้ใส่ $PATH: จะทำให้ path พัง  
วิธีแก้คือ
```
export PATH=/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:$PATH
```
