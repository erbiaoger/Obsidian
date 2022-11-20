## Par_file

### <center> simulation input parameters </center>

##### title of job
```markdown
title				=	Specfem2d
```
##### forward or adjont simulation

```markdown
SIMULATION_TYPE		=	1
<!-- 1 = forward, 2 = adjoint, 3 = both sumulataneously --> 
NOISE_TOMOGRAPHY	=	0
<!-- 0 = regular wave propagation simulation, 1/2/3 = noise simulation --> 
SAVE_FORWARD		=	.false.
<!-- save the last frame, needed for adjoint simulation --> 
```
##### parameters concerning partitioning
```markdown
NPROC				=	4
partitioning_method	=	3
```
##### number of control nodes pre element (4 or 9)
```markdown
ngnod				=	9
```
##### time step parameters
```markdown
NSTEP				=	1600
<!-- total number of time steps --> 
DT					=	1.1d-3
<!-- duration of a time step --> 
```
##### time stepping
```markdown
time_stepping_scheme=	1
<!-- 1 = Newmark, 2 = LDDRK4-6, 3 = classical RK4 4th-order 4-stage Runge-Kutta --> 
```
##### axisymmetric (2.5D) or Cartesian plannar (2D) simulation
```markdown
AXISYM				=	.false.
```
##### set the type of calculation (P_SV or SH/membrane waves)
```markdown
P_SV				=	.true.
```
##### set to true to use GPUs
```markdown
GPU_MODO			=	.false.
```
##### creates/reads a binary database that allows to skip all time consuming setup steps in initialization
```markdown
setup_with_binary_database	=	0
<!-- 0 = does not read/create database -->
<!-- 1 = creates database -->
<!-- 2 = reads database --> 
```
##### available models
```markdown
MODEL				=	default
<!-- default       - define model using nbmodels below -->
<!-- ascii         - read model from ascii database file -->
<!-- binary        - read model from binary databse file -->
<!-- binary_voigt  - read Voigt model from binary database file -->
<!-- external      - define model using define_external_model subroutine -->
<!-- gll           - read GLL model from binary database file -->
<!-- legacy        - read model from model_velocity.dat_input -->
SAVE_MODEL			=	default
<!-- Output the model with the requested type, does not save if turn to default or .false. -->
<!-- (available output formats: ascii, binary, gll, legacy) -->
```

### <center> attenuation </center>
##### attenuation parameters
```markdown
ATTENUATION_VISCOELASTIC	=	.false.
<!-- turn attenuation (viscoelasticity) on or off for non-poroelastic solid parts of the model --> 
<!-- 为模型的非多孔弹性实体部分打开或关闭衰减（粘弹性） --> 
ATTENUATION_VISCOACOUSTIC	=	.false.
<!-- turn attenuation (viscoacousticity) on or off for non-prooelastic fluid parts of the model --> 
<!-- 为模型的非弹性流体部分打开或关闭衰减（粘声性） --> 
```
##### for viscoelastic attenuation
```markdown
N_SLS						=	3
<!-- number of standard linear solids for attenuation (3 is usually the minimum) --> 
ATTENUATION_f0_REFERENCE	=	5.196
<!-- in case of attenuation, reference frequency in Hz at which the velocity values in the velcity model are givem (unused othervise); relevant only if source is a Dirac or a Heaviside, otherwise it is automatically set to f0 the dominant frequency of the source in the DATA/SOURCE file --> 
<!-- 在衰减的情况下，给出速度模型中速度值的参考频率（Hz）（未使用的其他方式）； 仅当源是 Dirac 或 Heaviside 时才相关，否则它会自动设置为 f0 数据/源文件中源的主频率 -->
READ_VELOCITIES_AI_f0		=	.false.
<!-- read seismic velocities at ATTENUATION_f0_REFERENCE instead of at infinite frequency (see user manual for more information) --> 
USE_SOLVOPT					=	.false.
<!-- use more precise but much more expensive way of determining the Q factor relaxation times, as in http://komatitsch.free.fr/preprints/GJI_Lombard_2016.pdf
 --> 
<!-- 使用更精确但更昂贵的方法来确定 Q 因子弛豫时间 --> 
```

##### for poroelastic attenuation
```markdown
ATTENUATION_PORO_FLUID_PART	=	.false.
<!-- turn viscous attenuation on or off for the fluid part of poroelastic parts of the model --> 
<!-- 打开或关闭模型多孔弹性部分的流体部分的粘性衰减 --> 
Q0_poroelastic				=	1
<!-- quality factor for viscous attenuation (ignore it if you are not using a poroelastic material) --> 
<!-- 粘性衰减的品质因数（如果您不使用多孔弹性材料，请忽略它） --> 
freq0_poroelastic			=	10
<!-- frequency for viscous attenuation (ignore it if you are not using a poroelastic material) --> 
<!-- 粘性衰减的频率（如果您不使用多孔弹性材料，请忽略它） --> 

<!-- to undo attenuation and/or PMLs for sensitivity kernel calculations or forward runs with SAVE_FORWARD -->
<!-- use the flag below. It performs undoing of attenuation and/or of PMLs in an exact way for sensitivity kernel calculations -->
<!-- but requires disk space for temporary storage, and uses a significant amount of memory used as buffers for temporary storage. -->
<!-- When that option is on the second parameter indicates how often the code dumps restart files to disk (if in doubt, use something between 100 and 1000). -->
<!-- 使用 SAVE_FORWARD 撤消衰减和/或 PML 以进行灵敏度内核计算或前向运行 -->
<!-- 使用下面的标志。 它以精确的方式执行衰减和/或 PML 的撤销以进行灵敏度核计算 -->
<!-- 但需要磁盘空间用于临时存储，并使用大量内存用作临时存储的缓冲区。 -->
<!-- 当该选项位于第二个参数上时，表示代码将重新启动文件转储到磁盘的频率（如果有疑问，请使用 100 到 1000 之间的值）。 -->
UNDO_ATTENUATION_AND_OR_PML	=	.false.
NT_DUMP_ATTENUATION			=	500

<!-- Instead of reconstructing the forward wavefield, this option reads it from the disk using asynchronous I/O. -->
<!-- Outperforms conventional mode using a value of NSTEP_BETWEEN_COMPUTE_KERNELS high enough. -->
<!-- 该选项不是重建前向波场，而是使用异步 I/O 从磁盘读取它。 -->
<!-- 使用足够高的 NSTEP_BETWEEN_COMPUTE_KERNELS 值优于传统模式。-->
NO_BACKWARD_RECONSTRUCTION	=	.false.
```

### <center> source </center>

##### source parameters
```markdown
NSOURCE			=	1
<!-- number of sources (source informfation is then read from the DATA/SOURCE file) --> 

force_normal_to+surface		=	.false.
<!-- angleforce normal to surface (external mesh and curve file needed) --> 
<!-- 垂直于表面的角力（需要外部网格和曲线文件）-->
<!-- use an existing initial wave field as source or start from zero (medium initially at rest) --> 
<!-- 使用现有的初始波场作为源或从零开始（介质最初处于静止状态）-->
initialfield				=	.false.
add_Bielak_conditions_bottom=	.false.
<!-- add Bielak conditions or not if initial plane wave --> 
<!-- 如果初始平面波是否添加 Bielak 条件 -->
add_Bielak_conditions_right	=	.false.
add_Bielak_conditions_top	=	.false.
add_Bielak_conditions_left	=	.false.
```
##### acoustic forcing
```markdown
ACOUSTIC_FORCING			=	.false.
<!-- acoustic forcing of an acoustic medium with a rigid interface --> 
<!-- 具有刚性界面的声学介质的声强迫 -->```
```

### <center> receivers </center>

##### receiver set parameters for recording stations (i.e. recording points)
```markdown
seismotype					=	1
<!-- record 1 = displ, 2 = veloc, 3 = accel, 4 = pressure, 5 = curl of displ, 6 = the fluid potential --> 
```
##### subsampling of the seismograms to create smaller files (butless accurately sampled in time)
<!-- 对地震图进行二次采样以创建更小的文件（但采样时间不太准确） -->
```markdown
subsamp_siesmos				=	1
```
##### so far, this option can only be used if all the receivers are in acoustic elements
<!-- 到目前为止，只有当所有接收器都在声学元中时才能使用此选项 --> 
```markdown
USE_TRICL_FOR_BETTER_PRESSURE	=	.false.
```
##### every how many time steps we save the seismograms
```markdown
<!-- (costly, do not use a very small value; if you use a very large value that is larger than the total number of time steps of the run, the seismograms will automatically be saved once at the end of the run anyway)<++> --> 
<!-- (代价高昂，不要使用非常小的值；如果使用的值大于运行的总时间步数，则无论如何都会在运行结束时自动保存一次地震图 ) -->
NSTEP_BETWEEN_OUTPUT_SEISMOS	=	1000
```
##### use this t0 as earliest satrting time rather than the automatically calculated one
<!-- 使用这个 t0 作为最早的开始时间而不是自动计算的时间 --> 
```markdown
USER_T0							=	0.0d0
```
##### seismogram formats
```markdown
save_ASCII_seismograms			=	.true.
<!-- save seismograms in ASCII format or not --> 
save_binary_seismograms_single	=	.true.
<!-- save seismograms in single precision binary format or not (can be used jointly with ASCII above to save both) --> 
save_binary_seismograms_double	=	.false.
<!-- save seismograms in double precision binary format or not (can be used jointly with both flags above to save all) --> 
SU_FORMAT						=	.false.
<!-- output single precision binary seismograms in Seismic Unix format (adjoint traces will be read in the same format) --> 
<!-- 以 Seismic Unix 格式输出单精度二进制地震图（以相同格式读取伴随轨迹） -->
```
##### use an existing STATION file found in ./DATA or create a new one from the receiver positions below in this Par_file
<!-- 使用在 ./DATA 中找到的现有 STATION 文件或从此 Par_file 中的以下接收器位置创建一个新文件 --> 
```markdown
use_existing_STATIONS			=	.false.
```
##### number of receiver sets (i.e. number of receiver lines to create below)
```markdown
nreceiversets					=	2
```
##### orientation
<!-- 方向 --> 
```markdown
anglerec						=	0.d0
<!-- angle to rotate components at receivers --> 
<!-- 在接收器处旋转组件的角度 -->
rec_normal_to_surface			=	.false.
<!-- base anglerec normal to surface (external mesh and curve file needed) --> 
<!-- 基础角度检波器与表面垂直（需要外部网格和曲线文件）-->
```
##### first receiver set (repeat these 6 lines and adjust nreceiversets accordingly)
```markdown
nrec							=	11
<!-- number of receivers --> 
xdeb							=	300.
<!-- first receiver x in meters --> 
zdeb							=	2200.
<!-- first receiver z in meters --> 
xfin							=	3700.
<!-- last receiver x in meters (ignored if only one receiver) --> 
zfin							=	2200.
<!-- last receiver z in meters (ignored if only one receiver) --> 
record_at_surface_same_vertical	=	.true.
<!-- receivers inside the medium or at the surface (z values are ignored if this is set to true, they are replaced with the topography height) --> 
<!-- 介质内部或表面的接收器（如果设置为 true，z 值将被忽略，它们会被地形高度替换）-->
```
##### second revceiver set
```markdown
nrec							=	11
xdeb							=	2500.
zdeb							=	2500.
xfin							=	1500.
zfin							=	0.
record_at_surface_same_vertical	=	.false.
```

### <center> adjoint kernel outputs </center>

##### save sensitivity kernels in ASCII format (much bigger files, but compatible with current GMT scripts) or in binary format
<!-- 以 ASCII 格式（更大的文件，但与当前的 GMT 脚本兼容）或二进制格式保存敏感内核 -->
```markdown
save_ASCII_kernels				=	.true.
```
##### since the accuracy of kernel integration may not need to respect the CFL, this option permits to save computing time, and memory with UNDO_ATTENUATION_AND_OR_PML mode
<!-- 由于内核集成的准确性可能不需要尊重 CFL，此选项允许使用 UNDO_ATTENUATION_AND_OR_PML 模式节省计算时间和内存 --> 
```markdown
NSTEP_BETEEN_COMPUTE_KERNELS	=	1
```
### <center> boundary confitions </center>

#### Perfectly Matched Layer (PML) boundaries
<!-- 完美匹配层 (PML) 边界 --> 
##### absorbings boundary active or not   
```markdown
PML_BOUNDARY_CONDITIONS			=	.true.
NELEM_PML_THICKNESS				=	3
ROTATE_PML_ACTIVATE				=	.false.
ROTATE_PML_ANGLE				=	30.
<!-- change the four parameters below only if you know what you are doing; they change the damping progiles inside the PMLs --> 
<!-- 仅在知道自己在做什么时才更改以下四个参数； 他们改变了 PML 内的阻尼特性 -->
K_MIN_PML						=	1.0d0
K_MAX_PML						=	1.0d0
damping_change_factor_acoustic	=	0.5d0
damping_change_factor_elastic	=	1.0d0
<!-- set the parameter below to .false. unless you know what you are doing; this implements automatic adjustment of the PML parametersfor elongated models. -->
<!-- 将下面的参数设置为 .false。 除非你知道自己在做什么； 这实现了细长模型的 PML 参数的自动调整。 -->
<!-- The goal is to improve the absorbing efficiency of PML for waves with large incidence angles, but this can lead to artefacts. --> 
<!-- 目标是提高 PML 对大入射角波的吸收效率，但这会导致伪影。 -->
<!-- In particular, this option is efficient only when the number of sources NSOURCES is equal to one --> 
<!-- 特别是，这个选项只有在源NSOURCES的数量等于1时才有效-->
PML_PARAMETER_ADJUSTMENT		=	.false.
```
##### Stacey ABC
```markdown
STACEY_ABSORBING_CONDITIONS		=	.false.
```
##### periodic boundaries
<!-- 周期性边界 --> 
```markdown
ADD_PERIODIC_CONDITIONS			=	.false.
PERIODIC_HORIZ_DIST				=	4000.d0
```
### <center>velocity and density models </center>

```markdown
nbmodels						=	4
<!-- available material types  --> 
<!-- 可用的材料类型 -->
<!-- acoustic:	model_number	1	rho	Vp	0	0	0	QKappa	9999	0	0	0	0	0	0	(for QKappa use 9999 to ignore it) --> 
<!-- elastic:	model_number	1	rho	Vp	Vs	0	0	QKappa	Qmu		0	0	0	0	0	0	(for QKappa and Qmu use 9999 to ignore them) --> 
<!-- when viscoelasticity or viscoacousticity is turned on, the Vp and Vs values that are read here are the UNTELAXED ones i.e. the values at infinite frequency unless the READ_VELOCITIES_AT_f0 parameter above is set to true, in which case they are the values at frequency f0 --> 
<!-- 当粘弹性或粘声性打开时，这里读取的 Vp 和 Vs 值是 UNTELAXED 的值，即无限频率的值，除非上面的 READ_VELOCITIES_AT_f0 参数设置为 true，在这种情况下它们是频率的值 f0 -->
<!-- Please also note that Qmu is always equal to Qs, but QKappa is in general not equal to Qp. To convert one to the other see doc/Qkappa_Qmu_versus_Qp_Qs_relationship_in_2D_plane_strain.pdf and utils/attenuation/conversion_from_Qkappa_Qmu_to_Qp_Qs_from_Dahlen_Tromp_959_960.f90. --> 
<!-- 还请注意，Qmu 总是等于 Qs，但 QKappa 通常不等于 Qp。 要将一个转换为另一个，请参阅 doc/Qkappa_Qmu_versus_Qp_Qs_relationship_in_2D_plane_strain.pdf 和 utils/attenuation/conversion_from_Qkappa_Qmu_to_Qp_Qs_from_Dahlen_Tromp_959_960.f90。 -->
<!-- acoustic:	model_number			1	rho	Vp	0	0	0	QKappa	9999	0	0	0	0	0	0	(for QKappa use 9999 to ignore it) --> 
<!-- elastic:	model_number			1	rho	Vp	Vs	0	0	QKappa	Qmu		0	0	0	0	0	0	(for QKappa and Qmu use 9999 to ignore them) --> 

<!-- anisotropic: model_number			2	rho	c11	c13 c15 c33 c35		c55		c12 c23 c25 0	0	0 -->
<!-- anisotropic in AXISYM: model_number2	rho c11 c13 c15 c33 c35		c55		c12 c23 c25 c22 0	0 -->
<!-- poroelastic: model_number			3	rhos rhof phi c kxx kxz		kzz		Ks	Kf	Kfr etaf mufr Qmu -->
<!-- tomo:        model_number			-1  0	0	A	0	0	0		0		0	0	0	0	0	0 -->
1 1 2700.d0 3000.d0 1732.051d0 0 0 9999 9999 0 0 0 0 0 0
2 1 2500.d0 2700.d0 0 0 0 9999 9999 0 0 0 0 0 0
3 1 2200.d0 2500.d0 1443.375d0 0 0 9999 9999 0 0 0 0 0 0
4 1 2200.d0 2200.d0 1343.375d0 0 0 9999 9999 0 0 0 0 0 0
```
##### external tomography file
```markdown
TOMEGRAPHY_FILE							=	./DATA/tomo_file.xyz
```
##### use an external mesh created by an external meshing tool or use the internal mesher
<!-- 使用由外部网格划分工具创建的外部网格或使用内部网格生成器 -->
```markdown
read_external_mesh						=	.false.
```
### PARAMETERS FOR EXTERNAL MESHING (外部网格参数)

##### data concerning mesh, when generated using third-party app 
<!-- 有关网格的数据，当使用第三方应用程序生成时 --> 
<!-- see also absorbing_conditions above --> 
```markdown
mesh_file								=	./DATA/mesh_file
<!-- file containing the mesh --> 
nodes_coords_file						=	./DATA/nodes_coords_file
<!-- file containing the nodes coordinates --> 
materials_file							=	./DATA/materials_file
<!-- file containing the material number for each element --> 
free_surface_file						=	./DATA/free_surface_file
<!-- file containing the free surface --> 
axial_elements_file						=	./DATAaxial_elements_file
<!-- file containing the axial elements if AXISYM is true --> 
absorbing_surface_file					=	./DATAabsorbing_surface_file
<!-- file containing the absorbing surface --> 
acoustic_forcing_surface_file			=	./DATA/MSH/Surf_acforcing_Botom_enforcing_mesh
<!-- file containing the acoustic forcing surface --> 
absorbing_cpml_file						=	./DATA/absorbjing_cpml_file
<!-- file containing the CPML element numbers --> 
tangential_detection_curve_file			=	./DATA/courbe_eros-nodes
<!-- file containing the curve delimiting the velocity model --> 
```
### PARAMETERS FOR INTERNAL MESHING (内部网格参数)

##### file containing interfaces for internal mesh 
```markdown
interfacesfile							=	./DATA/interfaces_simple_topo_curved.dat
```
##### geometry of the model (origin lower_left corner = 0,0) and mesh description
<!-- 模型的几何形状（原点左下角 = 0,0）和网格描述 --> 
```markdown
xmin		=	0.d0
<!-- abscissa of left side of the model (模型左侧横坐标) --> 
xmax		=	4000.d0
<!-- abscissa of right side of the model (模型右侧横坐标) --> 
nx			=	80
<!-- number of elements along X --> 
```
##### absorbing boundary parameters (see absorbing_conditions above)
```markdown
absorbbottom		=	.true.
absorbright			=	.true.
absorbtop			=	.false.
absorbleft			=	.true.
```
##### define the defferent regions of the model in the (nx, nz) spectral-element mesh
<!-- 在（nx，nz）谱元网格中定义模型的不同区域 --> 
```markdown
nbregions			=	5
<!-- then set below the different regions and model number for each region --> 
<!-- 然后在下面设置不同地区和每个地区的型号-->
<!-- format of each line :	nxmin	nxmax	nzmin	nzmax	material_number --> 
							1		80		1		20		1
							1		59		21		40		2
							71		80		21		40		2
							1		80		41		60		3
							60		70		21		40		4
```
### display parameters
##### 







