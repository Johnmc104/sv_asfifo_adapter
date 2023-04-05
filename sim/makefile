SIM = xrun#vcs xrun

FILE_LIST_PATH := ../sim_cfg/filelist		## file path
XRUN_TCL_PATH := ../sim_cfg/run.tcl		## xrun tcl patch

################
OPTION_XRUN := -64bit -sv -notimingcheck -access +rwc -accessreg +rwc -debug -uvmlinedebug -classlinedebug -plidebug -fsmdebug -uvmaccess -date -dumpstack -negdelay -timescale 1ns/100ps -lwdgen -f $(FILE_LIST_PATH) -input $(XRUN_TCL_PATH) -l xrun.log


OPTION_VCS := -f $(FILE_LIST_PATH)	\
	-timescale=1ns/1ps	\
	+define+DUMP	\
	-full64 +vc +v2k -sverilog -debug_access+all	\
	-debug_region+cell+encrypt	\
	-P ${VCS_VERDI1} ${VCS_VERDI2} | tee  vcs.log &

OPTION_Verdi := -f $(FILE_LIST_PATH) -ssf *.fsdb &
################


sim	:
	@echo "Welcome!"
ifeq ($(SIM),xrun)
	@echo "SIM is $(SIM) and dubug support indago"	
	@xrun $(OPTION_XRUN)
else
     ifeq ($(SIM),vcs)
	@echo "SIM is $(SIM) and dubug support verdi"
	@vcs $(OPTION_VCS)
     else
	@echo "SIM is $(SIM) and it not support now"
     endif
endif


indago	:
	@echo "Debug is indago"
	@indago
	@echo "Welcom indago !"

verdi	:
	@echo "Debug is verdi"
	@verdi $(OPTION_Verdi)
	@echo "Welcom verdi !"

clean:
	@echo "all files in vcs folder are cleaned "
	@rm -rf csrc simv.daidir simv xcelium.d ucli.key
	@rm -rf tb_top* *.log xrun.* .ida.db_tmp* ida* .indago* indago*

help	:
	@echo "Welcome"
	@echo "commoand:"
	@echo "make vcs/make verdi /make xrun/make indago/make cleanvcs/make cleanxrun"
	@echo "this template support vcs and xrun and default sim is xrun"
	@echo "this template support verdi and indgo to debug"
	@echo "you can use 'make sim SIM=vcs'to sim your project,and use 'make verdi' to debug"
	@echo "you can use 'make xrun' to sim,and use 'make indago' to debug"
	@echo "any question,you can email me about this VM"
