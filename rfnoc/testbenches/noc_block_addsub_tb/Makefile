#
# Copyright 2016 Ettus Research
#

#-------------------------------------------------
# Top-of-Makefile
#-------------------------------------------------
# Define BASE_DIR to point to the "top" dir
BASE_DIR = $(abspath ../../../../uhd-fpga/usrp3/top)
# BASE_DIR = /home/ejk/target_rfnoc/src/uhd-fpga/usrp3/top # EJK: Note this was included by rfnocmodtool. Not sure what the deal is here...
# Include viv_sim_preample after defining BASE_DIR
include $(BASE_DIR)/../tools/make/viv_sim_preamble.mak
include $(BASE_DIR)/../tools/make/viv_hls_ip_builder.mak

ARCH = zynq
PART_ID = xc7z020/clg484/-1

#-------------------------------------------------
# Testbench Specific
#-------------------------------------------------
# If simulation contains IP, define the IP_DIR and point
# it to the base level IP directory
OOT_DIR = $(abspath ../../)
FPGANNET_HLS_DIR = $(OOT_DIR)/hls

# Add HLS IP to build
include $(FPGANNET_HLS_DIR)/addsub/Makefile.inc

# Include makefile for HLS files 
RFNOC_SRCS += $(abspath \
$(HLS_IP_OUTPUT_SRCS) \
)

# Define only one toplevel module
SIM_TOP = noc_block_addsub_tb

# Add test bench, user design under test, and
# additional user created files
SIM_SRCS = \
$(abspath noc_block_addsub_tb.sv) \
$(abspath ../../fpga-src/noc_block_addsub.v)

#-------------------------------------------------
# Bottom-of-Makefile
#-------------------------------------------------
# Include all simulator specific makefiles here
# Each should define a unique target to simulate
# e.g. xsim, vsim, etc and a common "clean" target

hls_ip: $(HLS_IP_BUILD_TARGETS)

include $(BASE_DIR)/../tools/make/viv_simulator.mak
