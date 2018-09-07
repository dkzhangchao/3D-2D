  # 3D-2D
  1 #! /bin/bash
  2 set -e
  3 set -x
  4 
  5 scons -C ../../ -j12
  6 
  7 PARTITION_X=32
  8 PARTITION_Y=10
  9 TOTAL_MPI=$((PARTITION_X * PARTITION_Y))
 10 QUEUE=${QUEUE:-q_sw_share}
 11 
 12 bsub_job_name="sw-dh500-test"
 13 exec="../../bin/pmcl3d"
 14 #exec="./pmcl3d-sunway-gather-output-b6553d5-rank0-gather-and-write-snapshots"
 15 
 16 submit_cmd="/usr/sw-mpp/bin/bsub -I -b -m 1 -p -q  $QUEUE \
 17 -host_stack 1024 -share_size 7000 -n $TOTAL_MPI -cgsp 64 \
 18 -o bsub.out -J $bsub_job_name"
 19 #submit_cmd="/usr/sw-mpp/bin/bsub -I  -q  $QUEUE \
 20 #-n $TOTAL_MPI -o bsub.out -J $bsub_job_name"
 21 
 22 CMD="$submit_cmd   $exec \
 23   --NX 640 --NY 640 --NZ 120 -x $PARTITION_X -y $PARTITION_Y \ (网格大小)
 24   --TMAX 125.002 --DH 500.0 --DT 0.025 \ （总的时间长，网格间距，dt）
 25   --NSRC 13300 --NST 800 --READ_STEP 800 \ (源的总数，破裂)
 26   --READ_STEP_GPU 800 \
 27   --IFAULT 1 \ （1-线性 2-nolinear）
 28   --MESHP 1 \  (1 single file/ 0 文件夹／ 2 media.txt)
 29   --INSRC source \ (读取source这个单一文件)
 30   --NVE 1 \
 31   --MEDIASTART 2 \
 32   --NVAR 3 --INVEL input_rst \
 33   --NTISKP 50 \ (多少个快照输出一个文件)
 34   --WRITE_STEP 50 \ （多少步输出一个快照）相当于50*50输出一个动态图
 35   --FAC 1.0 --Q0 150. --EX 0.0 --FP 1.0 \ （震源的信息）
 36   --NBGX 1 --NEDX 640 \ （起始点，结束点）
 37   --NBGY 1 --NEDY 640 \
 38   --NBGZ 1 --NEDZ 1
 39 "
 40 
 41 rm -rf bsub.out output_ckp/* output_sfc/* && mkdir output_sfc output_ckp -p  ＃output_ckp 用于编译
 42 eval $CMD
 43 
 44 # od -f source | less 读取二进制文件 浮点数
 45 # od -d source | less 读取二进制文件 整数
 46 
 47 
 48 #CMD2="sfmath x=1.rsf y=c.rsf output=x-y | sfattr"
 49 #eval $CMD2


sfin < absobjs_1.rsf
sfwindow f3=3 n3=1  f2=2 n2=1 < shots.rsf > shots_3.rsf datapath=./
sfin < shots_3.rsf
./plot.sh shots_3
sfpen shots_3.vpl
sfgrey < shots_3.rsf > shots_3.vpl
sfpen shots_3.vpl






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






 
                              
                              
                              
                              
                               
