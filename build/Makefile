NAME = regulair

BOARD = icestick

DEVICE = 1k
PCF = $(NAME).pcf

QUIET = -q

all: $(NAME).bin

%.bin: %.txt
	icepack $< $@

%.txt: %.blif
	arachne-pnr $(QUIET) -d $(DEVICE) -o $@ -p $(PCF) $<

%.blif: %.v
	yosys $(QUIET) -p 'synth_ice40 -top main -blif $@' $<

%.v: FORCE
	python3 ../regulair.py

FORCE:

%.rpt: %.txt
	icetime -d hx$(DEVICE) -mtr $@ $<

upload: $(NAME).bin
	iceprog $<

explain: $(NAME).txt
	icebox_explain $<

clean:
	rm -f *.bin *.txt *.blif *.rpt *.v *.pcf


.PRECIOUS: %.bin %.txt %.blif %.v

.PHONY: all explain install clean
