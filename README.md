
opencl test tools

source is https://wiki.tiker.net/OpenCLHowTo


Testing

Download this file and unpack it:


curl https://codeload.github.com/hpc12/tools/tar.gz/master | tar xvfz -
Then compile the code:


cd tools-master
make
If your ICD loader and its header files (CL/cl.h) are in non-standard locations, you can say


make OPENCL_INC=/somewhere/include OPENCL_LIB=/somewhere/lib
Then run the following:


./print-devices
On my machine, this prints the following


platform 0: vendor 'Intel(R) Corporation'
  device 0: '       Intel(R) Core(TM) i7-2620M CPU @ 2.70GHz'
platform 1: vendor 'Advanced Micro Devices, Inc.'
  device 0: 'Intel(R) Core(TM) i7-2620M CPU @ 2.70GHz'
If the output is empty, then no ICDs were found, i.e. something went wrong with the installation.

To run a simple functional test of a device, do the following:


./cl-demo 1000000 10
You will be prompted for where to run. A sample session might look as follows--make sure it says 'GOOD' at the end:


Choose platform:
[0] Intel(R) Corporation
[1] Advanced Micro Devices, Inc.
Enter choice: 0
Choose device:
[0]        Intel(R) Core(TM) i7-2620M CPU @ 2.70GHz
Enter choice: 0
---------------------------------------------------------------------
NAME:        Intel(R) Core(TM) i7-2620M CPU @ 2.70GHz
VENDOR: Intel(R) Corporation
PROFILE: FULL_PROFILE
VERSION: OpenCL 1.1 (Build 31360.31426)
EXTENSIONS: cl_khr_fp64 cl_khr_icd cl_khr_global_int32_base_atomics cl_khr_global_int32_extended_atomics cl_khr_local_int32_base_atomics cl_khr_local_int32_extended_atomics cl_khr_byte_addressable_store cl_intel_printf cl_ext_device_fission cl_intel_exec_by_local_thread
DRIVER_VERSION: 1.1

Type: CPU
EXECUTION_CAPABILITIES: Kernel Native
GLOBAL_MEM_CACHE_TYPE: Read-Write (2)
CL_DEVICE_LOCAL_MEM_TYPE: Global (2)
SINGLE_FP_CONFIG: 0x7
QUEUE_PROPERTIES: 0x3

VENDOR_ID: 32902
MAX_COMPUTE_UNITS: 4
MAX_WORK_ITEM_DIMENSIONS: 3
MAX_WORK_GROUP_SIZE: 1024
PREFERRED_VECTOR_WIDTH_CHAR: 16
PREFERRED_VECTOR_WIDTH_SHORT: 8
PREFERRED_VECTOR_WIDTH_INT: 4
PREFERRED_VECTOR_WIDTH_LONG: 2
PREFERRED_VECTOR_WIDTH_FLOAT: 4
PREFERRED_VECTOR_WIDTH_DOUBLE: 2
MAX_CLOCK_FREQUENCY: 2700
ADDRESS_BITS: 64
MAX_MEM_ALLOC_SIZE: 2067921920
IMAGE_SUPPORT: 1
MAX_READ_IMAGE_ARGS: 480
MAX_WRITE_IMAGE_ARGS: 480
IMAGE2D_MAX_WIDTH: 8192
IMAGE2D_MAX_HEIGHT: 8192
IMAGE3D_MAX_WIDTH: 2048
IMAGE3D_MAX_HEIGHT: 2048
IMAGE3D_MAX_DEPTH: 2048
MAX_SAMPLERS: 480
MAX_PARAMETER_SIZE: 3840
MEM_BASE_ADDR_ALIGN: 1024
MIN_DATA_TYPE_ALIGN_SIZE: 128
GLOBAL_MEM_CACHELINE_SIZE: 64
GLOBAL_MEM_CACHE_SIZE: 262144
GLOBAL_MEM_SIZE: 8271687680
MAX_CONSTANT_BUFFER_SIZE: 131072
MAX_CONSTANT_ARGS: 480
LOCAL_MEM_SIZE: 32768
ERROR_CORRECTION_SUPPORT: 0
PROFILING_TIMER_RESOLUTION: 1
ENDIAN_LITTLE: 1
AVAILABLE: 1
COMPILER_AVAILABLE: 1
MAX_WORK_GROUP_SIZES: 1024 1024 1024
---------------------------------------------------------------------
*** Kernel compilation resulted in non-empty log message.
*** Set environment variable CL_HELPER_PRINT_COMPILER_OUTPUT=1 to see more.
*** NOTE: this may include compiler warnings and other important messages
***   about your code.
*** Set CL_HELPER_NO_COMPILER_OUTPUT_NAG=1 to disable this message.
0.001980 s
12.119479 GB/s
GOOD
The package also contains a simple interface helper (cl-helper.h and cl-helper.c) for OpenCL
