# Copyright (c) 2014-present, Facebook, Inc.
# All rights reserved.
#
# This source code is licensed in accordance with the terms specified in
# the LICENSE file found in the root directory of this source tree.

function(lzmaMain)
  set(library_root "${CMAKE_CURRENT_SOURCE_DIR}/src")

  add_library(thirdparty_lzma
    "${library_root}/src/common/tuklib_cpucores.c"
    "${library_root}/src/common/tuklib_physmem.c"
    "${library_root}/src/liblzma/check/check.c"
    "${library_root}/src/liblzma/check/crc32_fast.c"
    "${library_root}/src/liblzma/check/crc32_table.c"
    "${library_root}/src/liblzma/check/crc64_fast.c"
    "${library_root}/src/liblzma/check/crc64_table.c"
    "${library_root}/src/liblzma/check/sha256.c"
    "${library_root}/src/liblzma/common/alone_decoder.c"
    "${library_root}/src/liblzma/common/alone_encoder.c"
    "${library_root}/src/liblzma/common/auto_decoder.c"
    "${library_root}/src/liblzma/common/block_buffer_decoder.c"
    "${library_root}/src/liblzma/common/block_buffer_encoder.c"
    "${library_root}/src/liblzma/common/block_decoder.c"
    "${library_root}/src/liblzma/common/block_encoder.c"
    "${library_root}/src/liblzma/common/block_header_decoder.c"
    "${library_root}/src/liblzma/common/block_header_encoder.c"
    "${library_root}/src/liblzma/common/block_util.c"
    "${library_root}/src/liblzma/common/common.c"
    "${library_root}/src/liblzma/common/common.h"
    "${library_root}/src/liblzma/common/easy_buffer_encoder.c"
    "${library_root}/src/liblzma/common/easy_decoder_memusage.c"
    "${library_root}/src/liblzma/common/easy_encoder.c"
    "${library_root}/src/liblzma/common/easy_encoder_memusage.c"
    "${library_root}/src/liblzma/common/easy_preset.c"
    "${library_root}/src/liblzma/common/filter_buffer_decoder.c"
    "${library_root}/src/liblzma/common/filter_buffer_encoder.c"
    "${library_root}/src/liblzma/common/filter_common.c"
    "${library_root}/src/liblzma/common/filter_decoder.c"
    "${library_root}/src/liblzma/common/filter_encoder.c"
    "${library_root}/src/liblzma/common/filter_flags_decoder.c"
    "${library_root}/src/liblzma/common/filter_flags_encoder.c"
    "${library_root}/src/liblzma/common/hardware_cputhreads.c"
    "${library_root}/src/liblzma/common/hardware_physmem.c"
    "${library_root}/src/liblzma/common/index.c"
    "${library_root}/src/liblzma/common/index_decoder.c"
    "${library_root}/src/liblzma/common/index_encoder.c"
    "${library_root}/src/liblzma/common/index_hash.c"
    "${library_root}/src/liblzma/common/outqueue.c"
    "${library_root}/src/liblzma/common/stream_buffer_decoder.c"
    "${library_root}/src/liblzma/common/stream_buffer_encoder.c"
    "${library_root}/src/liblzma/common/stream_decoder.c"
    "${library_root}/src/liblzma/common/stream_encoder.c"
    "${library_root}/src/liblzma/common/stream_encoder_mt.c"
    "${library_root}/src/liblzma/common/stream_flags_common.c"
    "${library_root}/src/liblzma/common/stream_flags_decoder.c"
    "${library_root}/src/liblzma/common/stream_flags_encoder.c"
    "${library_root}/src/liblzma/common/vli_decoder.c"
    "${library_root}/src/liblzma/common/vli_encoder.c"
    "${library_root}/src/liblzma/common/vli_size.c"
    "${library_root}/src/liblzma/delta/delta_common.c"
    "${library_root}/src/liblzma/delta/delta_decoder.c"
    "${library_root}/src/liblzma/delta/delta_encoder.c"
    "${library_root}/src/liblzma/lz/lz_decoder.c"
    "${library_root}/src/liblzma/lz/lz_encoder.c"
    "${library_root}/src/liblzma/lz/lz_encoder_mf.c"
    "${library_root}/src/liblzma/lzma/fastpos_table.c"
    "${library_root}/src/liblzma/lzma/lzma2_decoder.c"
    "${library_root}/src/liblzma/lzma/lzma2_encoder.c"
    "${library_root}/src/liblzma/lzma/lzma_decoder.c"
    "${library_root}/src/liblzma/lzma/lzma_encoder.c"
    "${library_root}/src/liblzma/lzma/lzma_encoder_optimum_fast.c"
    "${library_root}/src/liblzma/lzma/lzma_encoder_optimum_normal.c"
    "${library_root}/src/liblzma/lzma/lzma_encoder_presets.c"
    "${library_root}/src/liblzma/rangecoder/price_table.c"
    "${library_root}/src/liblzma/simple/simple_coder.c"
    "${library_root}/src/liblzma/simple/simple_decoder.c"
    "${library_root}/src/liblzma/simple/simple_encoder.c"
    "${library_root}/src/liblzma/simple/x86.c"
  )

  # todo(alessandro): macOS and Windows support
  target_compile_definitions(thirdparty_lzma PRIVATE
    HAVE_CONFIG_H
    TUKLIB_GETTEXT=0
    LZMADEC
  )

  target_compile_options(thirdparty_lzma PRIVATE
    -include config.h
  )

  target_link_libraries(thirdparty_lzma PRIVATE
    thirdparty_c_settings
  )

  target_include_directories(thirdparty_lzma PRIVATE
    "${library_root}/src/liblzma"
    "${library_root}"
    "${library_root}/lib"
    "${library_root}/src/common"
    "${library_root}/src/liblzma/check"
    "${library_root}/src/liblzma/common"
    "${library_root}/src/liblzma/delta"
    "${library_root}/src/liblzma/lz"
    "${library_root}/src/liblzma/lzma"
    "${library_root}/src/liblzma/rangecoder"
    "${library_root}/src/liblzma/simple"
    "${CMAKE_CURRENT_SOURCE_DIR}/config"
    "${library_root}/src/liblzma/api"
  )

  target_include_directories(thirdparty_lzma SYSTEM INTERFACE
    "${library_root}/src/liblzma/api"
  )
endfunction()

lzmaMain()