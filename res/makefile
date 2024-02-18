

SHADERS				  = $(shell find shaders/* -maxdepth 1 | grep -E ".*/(vs|fs).*.sc")
SHADERS_OUT			= $(SHADERS:.sc=.$(SHADER_TARGET).bin)
SHADERC				  = ../build/lib/bgfx.cmake/cmake/bgfx/shaderc
SHADER_TARGET	  = metal
SHADER_PLATFORM = osx

%.$(SHADER_TARGET).bin: %.sc
	$(SHADERC)	--type $(shell echo $(notdir $@) | cut -c 1)						\
						  -i ../lib/bgfx.cmake/bgfx/src											\
							--platform $(SHADER_PLATFORM)							\
							-p $(SHADER_TARGET)										\
							--varyingdef $(dir $@)varying.def.sc					\
							-f $<													\
							-o $@

shaders: $(SHADERS_OUT)
