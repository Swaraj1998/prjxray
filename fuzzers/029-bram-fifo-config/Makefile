# Copyright (C) 2017-2020  The Project X-Ray Authors.
#
# Use of this source code is governed by a ISC-style
# license that can be found in the LICENSE file or at
# https://opensource.org/licenses/ISC
#
# SPDX-License-Identifier: ISC
N ?= 20

include ../fuzzer.mk

database: build/segbits_bramx.db

build/segbits_bramx.rdb: $(SPECIMENS_OK)
	${XRAY_SEGMATCH} -o build/segbits_bramx.rdb $(addsuffix /segdata_bram_[lr].txt,$(SPECIMENS))

build/segbits_bramx.db: build/segbits_bramx.rdb
	${XRAY_DBFIXUP} --db-root build --zero-db bits.dbf \
		--seg-fn-in build/segbits_bramx.rdb \
		--seg-fn-out build/segbits_bramx.db
	${XRAY_MASKMERGE} build/mask_bramx.db $(addsuffix /segdata_bram_[lr].txt,$(SPECIMENS))

pushdb:
	${XRAY_MERGEDB} bram_l build/segbits_bramx.db
	${XRAY_MERGEDB} bram_r build/segbits_bramx.db
	${XRAY_MERGEDB} mask_bram_l build/mask_bramx.db
	${XRAY_MERGEDB} mask_bram_r build/mask_bramx.db

.PHONY: database pushdb
