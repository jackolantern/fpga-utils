# FPGA Utils

A small collection of utilities to aid in FPGA development.


## mkrom
Create a Verilog ROM module from a data file.
```
$ ./mkrom --help
usage: mkrom [-h] --name NAME --depth DEPTH --width WIDTH --radix RADIX
             [--in INPATH] [--out OUTPATH] [--default DEFAULT] [--verbose]
             [--debug] [--arg-input-name INPNAME] [--arg-output-name OUTNAME]

Generate verilog rom module.

optional arguments:
  -h, --help            show this help message and exit
  --name NAME, -n NAME  The name of the generated module.
  --depth DEPTH, -d DEPTH
                        The depth of the generated rom.
  --width WIDTH, -w WIDTH
                        The width of the generated rom.
  --radix RADIX, -r RADIX
                        The radix of the input data. (Must be between 2, 8, 10, or 16.)
  --in INPATH, -i INPATH
                        The file to read from. (defaults to stdin)
  --out OUTPATH, -o OUTPATH
                        The file to write to. (defaults to stdout)
  --default DEFAULT     The default value for out of range data. (defaults to 0)
  --verbose             Verbose logging.
  --debug               Debug logging (very verbose).
  --arg-input-name INPNAME
                        The name of the input parameter. (defaults to inp)
  --arg-output-name OUTNAME
                        The name of the output parameter. (defaults to out)
```

### Data file format
A UTF-8 file containing the characters 0123456789abcdefABCDEF, whitespace, and
comments.  (The `#` character starts a line comment.)


### Data file example
```
# Example of an "image rom" with 3-bit color.
00666600 # This is supposed to be a "smiley face."
06666660
66066066 # This row is the eyes...
66666666
66666666
60666606 # These two rows are the "smile."
06000060 # Pretty cool, right?
00666600
00000000 # The rest of the rom is empty.
00000000
00000000
00000000
00000000
00000000
00000000
00000000
```

### Transformed data file:
```verilog
module image(inp, out);
	parameter DEPTH=7;
	parameter WIDTH=3;

	input [DEPTH-1:0] inp;
	output reg [WIDTH-1:0] out;

	always @* begin
		case (inp)
			7'b0000000: out = 3'o0;
			7'b0000001: out = 3'o0;
			7'b0000010: out = 3'o6;
			7'b0000011: out = 3'o6;
			7'b0000100: out = 3'o6;
			7'b0000101: out = 3'o6;
			7'b0000110: out = 3'o0;
			7'b0000111: out = 3'o0;
			7'b0001000: out = 3'o0;
			7'b0001001: out = 3'o6;
			7'b0001010: out = 3'o6;
			7'b0001011: out = 3'o6;
			7'b0001100: out = 3'o6;
			7'b0001101: out = 3'o6;
			7'b0001110: out = 3'o6;
			7'b0001111: out = 3'o0;
			7'b0010000: out = 3'o6;
			7'b0010001: out = 3'o6;
			7'b0010010: out = 3'o0;
			7'b0010011: out = 3'o6;
			7'b0010100: out = 3'o6;
			7'b0010101: out = 3'o0;
			7'b0010110: out = 3'o6;
			7'b0010111: out = 3'o6;
			7'b0011000: out = 3'o6;
			7'b0011001: out = 3'o6;
			7'b0011010: out = 3'o6;
			7'b0011011: out = 3'o6;
			7'b0011100: out = 3'o6;
			7'b0011101: out = 3'o6;
			7'b0011110: out = 3'o6;
			7'b0011111: out = 3'o6;
			7'b0100000: out = 3'o6;
			7'b0100001: out = 3'o6;
			7'b0100010: out = 3'o6;
			7'b0100011: out = 3'o6;
			7'b0100100: out = 3'o6;
			7'b0100101: out = 3'o6;
			7'b0100110: out = 3'o6;
			7'b0100111: out = 3'o6;
			7'b0101000: out = 3'o6;
			7'b0101001: out = 3'o0;
			7'b0101010: out = 3'o6;
			7'b0101011: out = 3'o6;
			7'b0101100: out = 3'o6;
			7'b0101101: out = 3'o6;
			7'b0101110: out = 3'o0;
			7'b0101111: out = 3'o6;
			7'b0110000: out = 3'o0;
			7'b0110001: out = 3'o6;
			7'b0110010: out = 3'o0;
			7'b0110011: out = 3'o0;
			7'b0110100: out = 3'o0;
			7'b0110101: out = 3'o0;
			7'b0110110: out = 3'o6;
			7'b0110111: out = 3'o0;
			7'b0111000: out = 3'o0;
			7'b0111001: out = 3'o0;
			7'b0111010: out = 3'o6;
			7'b0111011: out = 3'o6;
			7'b0111100: out = 3'o6;
			7'b0111101: out = 3'o6;
			7'b0111110: out = 3'o0;
			7'b0111111: out = 3'o0;
			7'b1000000: out = 3'o0;
			7'b1000001: out = 3'o0;
			7'b1000010: out = 3'o0;
			7'b1000011: out = 3'o0;
			7'b1000100: out = 3'o0;
			7'b1000101: out = 3'o0;
			7'b1000110: out = 3'o0;
			7'b1000111: out = 3'o0;
			7'b1001000: out = 3'o0;
			7'b1001001: out = 3'o0;
			7'b1001010: out = 3'o0;
			7'b1001011: out = 3'o0;
			7'b1001100: out = 3'o0;
			7'b1001101: out = 3'o0;
			7'b1001110: out = 3'o0;
			7'b1001111: out = 3'o0;
			7'b1010000: out = 3'o0;
			7'b1010001: out = 3'o0;
			7'b1010010: out = 3'o0;
			7'b1010011: out = 3'o0;
			7'b1010100: out = 3'o0;
			7'b1010101: out = 3'o0;
			7'b1010110: out = 3'o0;
			7'b1010111: out = 3'o0;
			7'b1011000: out = 3'o0;
			7'b1011001: out = 3'o0;
			7'b1011010: out = 3'o0;
			7'b1011011: out = 3'o0;
			7'b1011100: out = 3'o0;
			7'b1011101: out = 3'o0;
			7'b1011110: out = 3'o0;
			7'b1011111: out = 3'o0;
			7'b1100000: out = 3'o0;
			7'b1100001: out = 3'o0;
			7'b1100010: out = 3'o0;
			7'b1100011: out = 3'o0;
			7'b1100100: out = 3'o0;
			7'b1100101: out = 3'o0;
			7'b1100110: out = 3'o0;
			7'b1100111: out = 3'o0;
			7'b1101000: out = 3'o0;
			7'b1101001: out = 3'o0;
			7'b1101010: out = 3'o0;
			7'b1101011: out = 3'o0;
			7'b1101100: out = 3'o0;
			7'b1101101: out = 3'o0;
			7'b1101110: out = 3'o0;
			7'b1101111: out = 3'o0;
			7'b1110000: out = 3'o0;
			7'b1110001: out = 3'o0;
			7'b1110010: out = 3'o0;
			7'b1110011: out = 3'o0;
			7'b1110100: out = 3'o0;
			7'b1110101: out = 3'o0;
			7'b1110110: out = 3'o0;
			7'b1110111: out = 3'o0;
			7'b1111000: out = 3'o0;
			7'b1111001: out = 3'o0;
			7'b1111010: out = 3'o0;
			7'b1111011: out = 3'o0;
			7'b1111100: out = 3'o0;
			7'b1111101: out = 3'o0;
			7'b1111110: out = 3'o0;
			7'b1111111: out = 3'o0;
			default: out = 3'o0;
		endcase
	end
endmodule
```
