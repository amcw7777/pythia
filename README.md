#   How to set up PYTHIA in ROOT
##  Install ROOT at home:
```bash 
wget https://root.cern.ch/download/root_v5.34.36.source.tar.gz 
tar -zxf root_v5.34.36.source.tar.gz 
./configure 
make
source bin/thisroot.sh
echo "source bin/thisroot.sh" >> $HOME/.bashrc
```
##  Install PYTHIA
```bash
wget http://home.thep.lu.se/~torbjorn/pythia8/pythia8180.tgz
tar xvfz pythia8180.tgz
cd pythia8180
./configure --enable-shared -fPIC
make
echo "export PYTHIA8=$PWD" >> $HOME/.bashrc
echo "export PYTHIA8DATA=$PYTHIA8/xmldoc" >> $HOME/.bashrc
source $HOME/.bashrc
```
##  Recompile ROOT
```bash
cd $ROOTSYS
./configure --enable-pythia8 --with-pythia8-incdir=$PYTHIA8/include --with-pythia8-libdir=$PYTHIA8/lib
make
```
##  Test Pythia 
```bash
root -l root/tutorials/pythia/pythia8.C
```

##  Sometimes the error 
```bash
Error in <TInterpreter::TCling::AutoLoad>: failure loading library libEGPythia8.so for TPythia8
```
That means the libs need to be linked manually:
```bash
LD_LIBRARY_PATH=${PYTHIA8}/lib:${LD_LIBRARY_PATH}
DYLD_LIBRARY_PATH=${PYTHIA8}/lib:${DYLD_LIBRARY_PATH}
```
