# RASP WRF 3.6.1 compile

--install the intel compiler ** 
  ./install_GUI.sh   
   
  ** note: at first there was a multilib error 
   Protected multilib versions: libstdc++-4.8.5-16.el7_4.1.i686 != libstdc++-4.8.5-16.el7.x86_64 
   which was resolved by running: yum update libstdc++ 
    
 --install the intel mpi lib  
```
 cd l_mpi_2018.1.163   
 ./install_GUI.sh 
```

 --build the WRF v3.6.1 source 
 ```
 source /opt/intel/bin/ifortvars.sh intel64 
 source /opt/intel/bin/iccvars.sh intel64 
 setenv NETCDF /usr/local/netcdf 
 setenv WRFIO_NCD_LARGE_FILE_SUPPORT 1 
 ```
  
 --run ./configure, choose option 21 
 
   21.  Linux x86_64 i486 i586 i686, Xeon (SNB with AVX mods) ifort compiler with icc  (dm+sm) 
    
 --adjust the configure.wrf, add the compile optimizations, ref:  
 
 changed:  
 '''
 LDFLAGS_LOCAL   =       -O3 -xsse4.2 -convert big_endian $(OPTAVX) 
 FCOPTIM         =       -O3 -xsse4.2 -no-prec-div -no-prec-sqrt -fp-model fast=2 -mP2OPT_vec_xform_level=103 -qoverride-limits $(OPTAVX) 
 FCBASEOPTS      =       $(FCBASEOPTS_NO_G) -FR -cm -w -I. $(FCDEBUG) -convert big_endian 
  
  
solve_em.o : solve_em.F 
 
 
solve_em.o : 
	$(RM) $@ 
	$(SED_FTN) $*.F > $*.b  
	$(CPP) -I$(WRF_SRC_ROOT_DIR)/inc $(CPPFLAGS) $*.b  > $*.f90 
	$(RM) $*.b 
	$(FC) -O0 -xO -mP2OPT_vec_xform_level=103 -o $@ -c $(FCFLAGS) $(MODULE_DIRS) $(PROMOTION) $(FCSUFFIX) $(SOLVE_EM_SPECIAL) $(OMP) $*.f90 
```

 -- build wrf 
 
 make real_em 
  
 -- run wrf using intel's mpirun (adjusted the num_procs from 10 down to 6) 
 ```
ulimit -s unlimited 
set OMP_NUM_THREADS=6 
export KMP_STACKSIZE=100000000 
/opt/intel/impi/2018.1.163/bin64/mpirun -n 4 -ppn 2 /home/pj/WRF361/WRFV3/main/wrf.exe 
```
