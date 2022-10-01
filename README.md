# Masters


## Troubleshooting

### Illegal instruction (core dumped)

```
>>> import mujoco_py
>>> import os
>>> mj_path = mujoco_py.utils.discover_mujoco()
>>> xml_path = os.path.join(mj_path, 'model', 'humanoid.xml')
>>> model = mujoco_py.load_model_from_path(xml_path)
Illegal instruction (core dumped)
```
Propbably due to lack of resources

Check VM-machines CPU-info:
```
cat /proc/cpuinfo

processor	: 3
vendor_id	: GenuineIntel
cpu family	: 6
model		: 126
model name	: Intel(R) Core(TM) i7-1065G7 CPU @ 1.30GHz
stepping	: 5
microcode	: 0xffffffff
cpu MHz		: 1497.603
cache size	: 8192 KB
physical id	: 0
siblings	: 4
core id		: 3
cpu cores	: 4
apicid		: 3
initial apicid	: 3
fpu		: yes
fpu_exception	: yes
cpuid level	: 22
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni ssse3 cx16 pcid sse4_1 sse4_2 hypervisor lahf_lm invpcid_single ibrs_enhanced fsgsbase invpcid md_clear flush_l1d arch_capabilities
bugs		: spectre_v1 spectre_v2 spec_store_bypass swapgs itlb_multihit mmio_stale_data retbleed
bogomips	: 2995.20
clflush size	: 64
cache_alignment	: 64
address sizes	: 39 bits physical, 48 bits virtual
```
Note: No Avx or Avx2 under flags. According to intels webpage Intel(R) Core(TM) i7-1065G7 CPU @ 1.30GHz should be able to have AVX2 and AVX512

Trying to enable AVX2 by disabling Hyper-V (the turtle lower right corner) according to https://stackoverflow.com/questions/65780506/how-to-enable-avx-avx2-in-virtualbox-6-1-16-with-ubuntu-20-04-64bit:

1. Open Command Prompt in Windows Host as Adm.
2. Disabel Hypervisor launch ``` bcdedit /set hypervisorlaunchtype off```
3. Shutdown
4. Wait a few seconds before starting the computer

Note: I did not have to Disable Microsoft Hyper-V after disabling Hypervisor launch. 

This worked and the error disappeared.







