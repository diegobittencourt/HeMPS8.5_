COR  =\033[0;32m
NC   =\033[0m # No Color

CFLAGS = -D_GLIBCXX_USE_CXX11_ABI=0

#systemc g++ compiler
SC_C = g++ -c -g -Wall -O2 -fpermissive -Wno-write-strings $(CFLAGS)
#HEMPS_TGT=$(HEMPS_TGT)
HEMPS_TGT=$(notdir $(patsubst %/,%,$(dir $(CURDIR))))


#SystemC files
TOP 		=hemps test_bench
PE	 		=pe
DMNI 		=dmni
MEMORY 		=ram
PROCESSOR 	=mlite_cpu
ROUTER	 	=queue switchcontrol router_cc

TOP_SRC	    	= $(addprefix sc/, 						$(TOP:=.cpp)  $(TOP:=.h) 			)
PE_SRC			= $(addprefix sc/pe/, 					$(PE:=.cpp) $(PE:=.h)  				)
DMNI_SRC		= $(addprefix sc/pe/dmni/, 				$(DMNI:=.cpp) $(DMNI:=.h)			)
MEMORY_SRC		= $(addprefix sc/pe/memory/,			$(MEMORY:=.cpp) $(MEMORY:=.h)		) 
PROCESSOR_SRC	= $(addprefix sc/pe/processor/plasma/, 	$(PROCESSOR:=.cpp) $(PROCESSOR:=.h)	)
ROUTER_SRC		= $(addprefix sc/pe/router/, 			$(ROUTER:=.cpp) $(ROUTER:=.h)		)

TOP_TGT 		=$(TOP:=.o)
PE_TGT	 		=$(PE:=.o)
DMNI_TGT 		=$(DMNI:=.o)
MEMORY_TGT 		=$(MEMORY:=.o)
PROCESSOR_TGT 	=$(PROCESSOR:=.o)
ROUTER_TGT	 	=$(ROUTER:=.o)

all: $(HEMPS_TGT)
	@cp $(HEMPS_TGT) ../

$(HEMPS_TGT): $(ROUTER_TGT) $(PROCESSOR_TGT) $(DMNI_TGT) $(MEMORY_TGT) $(PE_TGT) $(TOP_TGT)
	@printf "${COR}Generating %s ...${NC}\n" "$@"
	g++ -I./ -o $@ $^ -L. -L/soft64/util/accelera/systemc/2.3.1/lib-linux64 -lsystemc
	
$(TOP_TGT): $(TOP_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp

$(PE_TGT): $(PE_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp

$(DMNI_TGT): $(DMNI_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp

$(MEMORY_TGT): $(MEMORY_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp

$(PROCESSOR_TGT): $(PROCESSOR_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp

$(ROUTER_TGT): $(ROUTER_SRC)
	@printf "${COR}Compiling SystemC source: %s ...${NC}\n" "$(dir $<)$*.cpp"
	$(SC_C) $(dir $<)$*.cpp
	

clean:
	@printf "Cleaning up\n"
	@rm -f *~
	@rm -f *.o
	@rm -f *.exe
	@rm -f HeMPS
	@rm -f repository*
