PLUSARGS += "+UVM_VERBOSITY=UVM_MEDUIM"
TOPLEVEL := top
MODULE   ?= top_module
AHB_FILES ?= $(PWD)/../../hdl/rtl/bus_wrapper/EF_PSRAM_CTRL_AHBL.v
APB_FILES ?= # TODO: Add add APB wrapper file path
WB_FILES ?= # TODO: Add add WB wrapper file path
HDL_FILES ?= $(PWD)/../../hdl/rtl/EF_PSRAM_CTRL.v
VIP_FILES ?= $(PWD)/23LC1024.v
VERILOG_SOURCES ?=  $(PWD)/top.v $(AHB_FILES) $(HDL_FILES) $(VIP_FILES)
RTL_MACROS += "" # Add macros needed
BUS_TYPE ?= AHB
RTL_MACROS += -DBUS_TYPE_AHB
DESIGN_NAME = EF_PSRAM_CTRL_AHBL
export CLK_MAKEFILE = HCLK
export RST_MAKEFILE = HRESETn
## netlist Gen 
GL_MACROS += -DGL -DFUNCTIONAL  $(RTL_MACROS) -DUNIT_DELAY=\#1 
PRE_SYS_FILES = $(AHB_FILES) $(APB_FILES) $(WB_FILES) $(HDL_FILES)
PDK_DIR = $(HOME)/.volare/volare/sky130/versions/bdc9412b3e468c102d01b7cf6337be06ec6e9c9a/sky130A/
PDK_FILES = $(PDK_DIR)/libs.ref/sky130_fd_sc_hd/verilog/primitives.v $(PDK_DIR)/libs.ref/sky130_fd_sc_hd/verilog/sky130_fd_sc_hd.v # get this from openlane logs in the future 
IPM_DIR = $(HOME)/.ipm
POST_SYS_FILES = $(PWD)/top.v $(VIP_FILES) $(PWD)/../../hdl/gl/synthesis/nl/$(DESIGN_NAME).nl.v

# ifeq ($(BUS_TYPE),APB)
#     RTL_MACROS += -DBUS_TYPE_APB
# else ifeq ($(BUS_TYPE),AHB)
#     RTL_MACROS += -DBUS_TYPE_AHB
# else ifeq ($(BUS_TYPE),WISHBONE)
#     RTL_MACROS += -DBUS_TYPE_WISHBONE
# endif
# RTL_MACROS ?= "-DSKIP_WAVE_DUMP"
YAML_FILE = $(PWD)/../../EF_PSRAM_CTRL.yaml # TODO: update yaml file path
MAKEFLAGS += --no-print-directory

# List of tests
TESTS := psram_spi_test psram_sqi_test psram_hsize_test

# Variable for tag - set this as required
SIM_TAG ?= default_tag

# Define SIM_PATH variable
SIM_PATH := $(PWD)/sim/$(SIM_TAG)

# Check and clone EF_UVM repository at the beginning of the Makefile execution

clone_ef_uvm := $(shell if [ ! -d "EF_UVM" ]; then \
	echo "Cloning the EF_UVM repository..."; \
	git clone https://github.com/efabless/EF_UVM.git; \
fi;)


include EF_UVM/Makefile.test
