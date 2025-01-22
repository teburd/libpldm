# Copyright (c) 2024 Intel Corporation.
#
# SPDX-License-Identifier: BSD-3-Clause

if(CONFIG_PLDM)
	set(PLDM_ROOT ${CMAKE_CURRENT_SOURCE_DIR}/..)

	zephyr_interface_library_named(pldm)
	target_link_libraries(zephyr_interface INTERFACE pldm)
	target_include_directories(pldm INTERFACE ${PLDM_ROOT}/include)
	target_include_directories(pldm INTERFACE ${PLDM_ROOT}/src)

	zephyr_library_named(modules_pldm)
	zephyr_library_link_libraries(pldm)

	zephyr_library_sources_ifdef(
		CONFIG_PLDM
		${PLDM_ROOT}/src/utils.c
		${PLDM_ROOT}/src/responder.c

		${PLDM_ROOT}/src/requester/instance-id.c
		${PLDM_ROOT}/src/requester/pldm.c

		${PLDM_ROOT}/src/dsp/base.c
		${PLDM_ROOT}/src/dsp/bios.c
		${PLDM_ROOT}/src/dsp/bios_table.c
		${PLDM_ROOT}/src/dsp/firmware_update.c
		${PLDM_ROOT}/src/dsp/fru.c
		${PLDM_ROOT}/src/dsp/pdr.c
		${PLDM_ROOT}/src/dsp/platform.c

		${PLDM_ROOT}/src/transport/af-mctp.c
		${PLDM_ROOT}/src/transport/mctp-demux.c
		${PLDM_ROOT}/src/transport/socket.c
		${PLDM_ROOT}/src/transport/test.c
		${PLDM_ROOT}/src/transport/transport.c
	)
endif() 
