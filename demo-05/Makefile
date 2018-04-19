abspath_to_makefile := $(abspath $(lastword $(MAKEFILE_LIST)))
makefile_dir := $(patsubst %/,%,$(dir $(abspath_to_makefile)))

title := demo
wav_file := $(makefile_dir)/$(title).wav

.PHONY: all
all: $(wav_file)

orchestra := $(makefile_dir)/orchestra
score := $(makefile_dir)/score

subdirs := aux bus envelope instrument oscillator part plugin util
includes := $(foreach subdir,$(subdirs),$(wildcard $(makefile_dir)/$(subdir)/*))

csound_flags := -B 1024 -b 256 --dither --ksmps=1 -m 135 -s

sample_rate := 44100
csound_flags += -r $$((4 * $(sample_rate)))

$(wav_file): $(orchestra) $(score) $(includes)
	csound $(csound_flags) -o temp -W $(orchestra) $(score); \
	trap 'rm -f temp' EXIT; \
	sndfile-resample -c 0 -to $(sample_rate) temp $(wav_file)

.PHONY: clean
clean:
	rm -f $(wav_file)
