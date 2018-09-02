

Marmosi model:
```
  cp -r data/marm ~/
  mkdir -p job/01
  cd job
  vim README.md   # write some comments about case 01
  cd 01
  cp ../../model/marm/* .
  vim SConstruct  # update the parameters is necessary
  vim run.sh      # choose the task you want to start
  ./run.sh				
```

BP model (multi-scale FWI):
```
case 2:
  cp -r data/bp ~/
  mkdir -p job/02
  cd job
  cd 02
  cp ../../model/bp20/* .
  ./scons.sh
  ./multi.sh
  
######
Full frequency
scons: Reading SConscript files ...
scons: done reading SConscript files.
scons: Building targets ...
scons: `vel_t0.rsf' is up to date.
< vel_t0.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f1=0 n1=96 f2=0 n2=540 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfput label1=Depth unit1=m label2=Lateral unit2=m > vel_t1.rsf
< vel_t1.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f2=0 n2=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfspray axis=2 n=270 > vel_x0.rsf
< vel_t1.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f2=539 n2=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfspray axis=2 n=270 > vel_x1.rsf
< vel_x0.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfcat axis=2 vel_t1.rsf vel_x1.rsf > vel_t2.rsf
< vel_t2.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f1=95 n1=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfspray axis=1 n=32 > vel_z1.rsf
< vel_t2.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfcat axis=1 vel_z1.rsf > vel.rsf
< vel.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfmath output="1/input" | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfsmooth rect1=5 rect2=750 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfmath output="1/input" > smvel.rsf
< vel.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Marmousi model" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel.vpl
< smvel.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Smoothed model" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > smvel.vpl
scons: `Fig/marm.vpl' is up to date.
/usr/sw-mpp/bin/bsub -I -q q_x86_share -n 1 -o bsub.out -J "essfwi" ./essfwi-damp-7-x vin=smvel.rsf shots=shots.rsf vreal=vel.rsf vout=vsnaps.rsf absobjs=absobjs.rsf norobjs=norobjs.rsf niter=600 seed=10 maxdv=200 nita=15 flo=0 fhi=-1
Job <43512972> has been submitted to queue <q_x86_share>



Job 43523496 has been finished.
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=49 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 50" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel50.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=99 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 100" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel100.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=199 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 200" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel200.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=299 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 300" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel300.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=399 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 400" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel400.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=499 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 500" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel500.vpl
< vsnaps.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfwindow f3=599 n3=1 | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgrey title="Essfwi, iter 600" color=j allpos=y pclip=100 bias=1500 gainpanel=1 scalebar=y barreverse=y barunit=m/s barlabel=Velocity > vel600.vpl
/home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/vppen size=r vpstyle=n gridnum=4,2 vel50.vpl vel100.vpl vel200.vpl vel300.vpl vel400.vpl vel500.vpl vel600.vpl > essvelset.vpl
< absobjs.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfput n2=1 label1=Iteration unit1= unit2= label2= | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgraph title="Absolute objective value" dash=0 plotfat=5 grid=y yreverse=n > absobjs.vpl
< norobjs.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfput n2=1 label1=Iteration unit1= unit2= label2= | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgraph title="Normalized objective value" dash=0 plotfat=5 grid=y yreverse=n > norobjs.vpl
/usr/sw-mpp/bin/bsub -I -q q_x86_share -n 1 -o bsub.out -J "norm" ../../bin/norm realvel=vel.rsf velset=vsnaps.rsf l1norm=l1norm.rsf l2norm=l2norm.rsf
Job <43523718> has been submitted to queue <q_x86_share>
waiting for dispatch ...
dispatching ...
Current working dir: /home/export/online1/swyf/swcbw/projects/swfwi/job_201804/bp_linear_017
Job 43523718 has been finished.
< l1norm.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfput n2=1 label1=Iteration unit1= unit2= label2= | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgraph title="l1norm" dash=0 plotfat=5 grid=y yreverse=n > l1norm.vpl
< l2norm.rsf /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfput n2=1 label1=Iteration unit1= unit2= label2= | /home/export/online1/swyf/swcbw/softs/install_new/madagascar-1.6.4/bin/sfgraph title="l2norm" dash=0 plotfat=5 grid=y yreverse=n > l2norm.vpl
scons: done building targets.
Current frequency is 2Hz





# niagara account
log in:
ssh zhang18@niagara.computecanada.ca




# 3D-2D

scp -r zhangchao@222.195.79.32:~


 cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/fkSem_Tong/submit_job/
 
 cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/fkSem_Fang/submit_job/
 
 
 gfortran  -std=gnu -fimplicit-none -frange-check -O2 -pedantic -pedantic-errors -Waliasing -Wampersand -Wline-truncation -Wsurprising -Wunderflow -ffree-line-length-132 -I../../setup -c -o ../../obj/specfem2D.o ./specfem2D.F90
 
 
 
 ssh -X zhang18@login.scinet.utoronto.ca
 ssh zhangc@128.100.79.35 -X
 ssh zhangchao@222.195.76.41
 
 
 
 ssh -X  gpc03
 
 cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF/submit_job
 
 cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiSYN1/submit_job 
 
  
 cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiSYN/submit_job 
 
 cd /scratch/l/liuqy/zhang18/seisDD/seisDD/SRC
 
vim /scratch/l/liuqy/zhang18/seisDD/seisDD/SRC/misfit_adjoint.f90

vim /scratch/l/liuqy/zhang18/seisDD/seisDD/SRC/data_misfit.f90

cd  /scratch/l/liuqy/zhang18/seisDD/seisDD/lib

vim  /scratch/l/liuqy/zhang18/seisDD/seisDD/lib/src/adjoint_lib.f90 

vim /scratch/l/liuqy/zhang18/seisDD/seisDD/lib/src/constants.f90 

cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang_smooth/submit_job

cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang_gauss/submit_job

cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang_line2/submit_job/

cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang_line1_LVZ/submit_job/

scp zhang18@login.scinet.utoronto.ca:/scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang_smooth/submit_job/RESULTS/invesion/Scale0_CC_AD/misfit_kernel/*beta_kernel_smooth*

cd /scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang/submit_job/RESULTS/invesion/Scale0_CC_AD

scp zhang18@login.scinet.utoronto.ca:/scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang/submit_job/RESULTS/invesion/Scale0_CC_AD/misfit_kernel/*beta_kernel_smooth*

scp zhang18@login.scinet.utoronto.ca:/scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang/submit_job/RESULTS/invesion/Scale0_CC_AD/m_6/*vs*

scp -r zhang18@login.scinet.utoronto.ca:/scratch/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang/submit_job/FwiEGF_fang/000000/DATA_*


mpirun -np 4 ./bin/misfit_adjoint.exe true z CC AD /oldscratch/l/liuqy/zhang18/seisDD/GJI2016/FwiSYN/submit_job/FwiSYN//000000/

mpirun -np 4 ./bin/misfit_adjoint.exe true z CC AD /sgfs1/scratch3/l/liuqy/zhang18/seisDD/GJI2016/FwiEGF_fang/submit_job/FwiEGF_fang//000000/

mpirun -np 4 ./bin/misfit_adjoint.exe true z MT AD /sgfs1/scratch3/l/liuqy/zhang18/seisDD/GJI2016/FwiSGF/submit_job/FwiSGF/000000/






 
                              
                              
                              
                              
                               
