# Master makefile for DL_POLY Quantum
# 
#=======================================================================
# Define default settings
#=======================================================================

BINROOT = ../execute
CC  = gcc
EX = DLPOLY.X
EXE = $(BINROOT)/$(EX)
FC=mpif90
SHELL=/bin/sh
TYPE=par

#=====================================================================
# Define object files

OBJ_MOD = parse_module.o setup_module.o error_module.o \
	site_module.o config_module.o pair_module.o utility_module.o\
        water_module.o \
        pimd_module.o metafreeze_module.o solvation_module.o tether_module.o \
	vdw_module.o property_module.o rigid_body_module.o \
	angles_module.o bonds_module.o shake_module.o \
	inversion_module.o dihedral_module.o core_shell_module.o \
	exclude_module.o ewald_module.o hkewald_module.o coulomb_module.o\
	external_field_module.o four_body_module.o \
	metal_module.o nhc_module.o ensemble_tools_module.o \
	temp_scalers_module.o three_body_module.o spme_module.o \
	tersoff_module.o neu_coul_module.o \
	nlist_builders_module.o forces_module.o \
	lf_motion_module.o lf_rotation1_module.o \
	lf_rotation2_module.o vv_motion_module.o \
	pimd_piglet_module.o \
	vv_rotation1_module.o vv_rotation2_module.o vv_pimd_module.o\
	pmf_module.o integrator_module.o optimiser_module.o \
	hyper_dynamics_module.o driver_module.o \
	define_system_module.o correlation_module.o

OBJ_SRC = dlpoly.o

OBJ_PAR = basic_comms.o merge_tools.o pass_tools.o

#=====================================================================
# Define targets
all:
	@echo "Error - please specify a target machine!"
	@echo "Permissible targets for this Makefile are:"
	@echo "                                          "
	@echo "debug                      (parallel)"
	@echo "dlpoly                     (parallel)"
	@echo "         "
	@echo "Please examine Makefile for details"

# system specific targets follow :

#=================== debug ===========================================
debug:
	$(MAKE) FC="mpif90" LD="mpif90 -o" \
	LDFLAGS="-O2 -g -ffast-math -fcheck=bounds" \
	FFLAGS="-c -O2 -g -ffast-math -fcheck=bounds" \
	EX=$(EX) BINROOT=$(BINROOT) $(TYPE)

#=================== Dlpoly ==========================================
dlpoly:
	$(MAKE) LD="mpif90 -o" LDFLAGS="-lblas -llapack " \
	FC=mpif90 FFLAGS?="-c -O2" \
	EX=$(EX) BINROOT=$(BINROOT) $(TYPE)

#=====================================================================
# Default code for parallel (MPI) execution

par: check $(OBJ_MOD) $(OBJ_PAR) $(OBJ_SRC)
	$(LD) $(EX) $(LDFLAGS) $(OBJ_MOD) $(OBJ_PAR) $(OBJ_SRC)
	mv $(EX) $(EXE)

#=====================================================================
# Check that a machine has been specified
check:
	@if test $(FC) = "undefined";\
	then echo "You must specify a target machine!"; \
	exit 99;\
	fi

#=====================================================================
# Clean up the source directory
clean:
	rm -f $(OBJ_MOD) $(OBJ_PAR) $(OBJ_SRC) *.mod $(EXE)

#=====================================================================
# Declare dependencies
.f.o: 
	$(FC) $(FFLAGS) $*.f
.c.o: 
	$(CC) -c $*.c

#=====================================================================
# Declare dependency on module files

$(OBJ_SRC): $(OBJ_MOD)

# utility_module.o: config_module.o
# water_module.o: config_module.o
# metafreeze_module.o: setup_module.o
# pimd_module.o: setup_module.o
# error_module.o: setup_module.o
# site_module.o: error_module.o
# setup_module.o: parse_module.o
# config_module.o: setup_module.o
# solvation_module.o: setup_module.o
# pair_module.o: setup_module.o
# tether_module.o: config_module.o
# property_module.o: config_module.o
# vdw_module.o: config_module.o
# bonds_module.o: config_module.o
# angles_module.o: config_module.o
# rigid_body_module.o: config_module.o
# dihedral_module.o: config_module.o
# inversion_module.o: config_module.o
# shake_module.o: error_module.o
# pair_module.o: error_module.o
# config_module.o: error_module.o
# pimd_module.o: config_module.o
# metafreeze_module.o: utility_module.o
# pimd_module.o: water_module.o
# property_module.o: tether_module.o
# angles_module.o: property_module.o
# ewald_module.o: exclude_module.o
# coulomb_module.o: ewald_module.o
# lf_rotation1_module.o: lf_motion_module.o
# lf_rotation2_module.o: lf_rotation1_module.o
# vv_rotation2_module.o: vv_rotation1_module.o
# integrator_module.o: pmf_module.o
# exclude_module.o: angles_module.o
# core_shell_module.o: config_module.o
# hkewald_module.o: config_module.o
# external_field_module.o: config_module.o
# metal_module.o: config_module.o
# four_body_module.o: config_module.o
# nhc_module.o: error_module.o
# ensemble_tools_module.o: setup_module.o
# temp_scalers_module.o: config_module.o
# three_body_module.o: config_module.o
# tersoff_module.o: config_module.o
# spme_module.o: config_module.o
# neu_coul_module.o: config_module.o
# nlist_builders_module.o: config_module.o
# forces_module.o: config_module.o
# pimd_piglet_module.o: setup_module.o
# lf_motion_module.o: config_module.o
# vv_motion_module.o: config_module.o
# vv_pimd_module.o: setup_module.o
# pmf_module.o: config_module.o
# vv_rotation1_module.o: config_module.o
# driver_module.o: config_module.o
# optimiser_module.o: config_module.o
# hyper_dynamics_module.o: config_module.o
# correlation_module.o: setup_module.o
# pass_tools.o: setup_module.o
# basic_comms.o: setup_module.o
# merge_tools.o: error_module.o
# define_system_module.o: angles_module.o
# pimd_piglet_module.o: pimd_module.o
# ensemble_tools_module.o: config_module.o
# solvation_module.o: error_module.o
# correlation_module.o: config_module.o
# vv_pimd_module.o: config_module
# pass_tools.o: error_module.o
# solvation_module.o: config_module.o
# shake_module.o: site_module.o
# merge_tools.o: core_shell_module.o
# vdw_module.o: metafreeze_module.o
# water_module.o: utility_module.o
# tether_module.o: utility_module.o
# rigid_body_module.o: solvation_module.o 
# bonds_module.o: metafreeze_module.o
# core_shell_module.o: property_module.o 
# dihedral_module.o: metafreeze_module.o
# inversion_module.o: metafreeze_module.o
# four_body_module.o: metafreeze_module.o
# hkewald_module.o: exclude_module.o
# external_field_module.o: utility_module.o
# metal_module.o: property_module.o
# ensemble_tools_module.o: core_shell_module.o
# temp_scalers_module.o: core_shell_module.o
# spme_module.o: utility_module.o
# three_body_module.o: metafreeze_module.o
# neu_coul_module.o: ewald_module.o
# tersoff_module.o: utility_module.o
# lf_motion_module.o: ensemble_tools_module.o
# forces_module.o: coulomb_module.o
# nlist_builders_module.o: exclude_module.o
# vv_motion_module.o: ensemble_tools_module.o
# optimiser_module.o: rigid_body_module.o
# vv_rotation1_module.o: ensemble_tools_module.o
# pmf_module.o: ensemble_tools_module.o
# driver_module.o: forces_module.o
# hyper_dynamics_module.o: ensemble_tools_module.o
# correlation_module.o: utility_module.o
# shake_module.o: solvation_module.o
