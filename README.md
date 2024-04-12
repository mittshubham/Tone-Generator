# Tone-Generator
LIBRARY IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity TONE_GENERATOR is
    Port (
        CLK : in std_logic;
        RSTN : in std_logic;
 TONE : in std_logic;
        TONE_OUT : out std_logic
    );
end TONE_GENERATOR;

architecture FUNCTIONALITY of TONE_GENERATOR is

type ARR_TYPE_OCTAVE is array (0 to 7) of integer range 0 to 7;

signal SA,RE,GA,MA,PA,DHA,NI,SA1 : std_logic :='0';
signal COUNT_SA : integer range 0 to 95555 := 0;
signal COUNT_RE : integer range 0 to 85132 := 0;
signal COUNT_GA : integer range 0 to 75843 :=0;
signal COUNT_MA : integer range 0 to 71586 := 0;
signal COUNT_PA : integer range 0 to 63776 := 0;
signal COUNT_DHA : integer range 0 to 56818 := 0;
signal COUNT_NI : integer range 0 to 50620 := 0;
signal COUNT_SA1 : integer range 0 to 47778 := 0;
signal COUNT_TONE : integer range 0 to 25000000 := 0;
signal COUNT_MASTER : integer range 0 to 25 := 0;

constant OCTAVE : ARR_TYPE_OCTAVE := (0,1,2,3,4,5,6,7);

begin

process(CLK)
begin
if RSTN = '0' then
COUNT_SA <= 0;
COUNT_RE <= 0;
COUNT_GA <= 0;
COUNT_MA <= 0;
COUNT_PA <= 0;
COUNT_DHA <= 0;
COUNT_NI <= 0;
COUNT_SA1 <= 0;
COUNT_TONE <= 0;
COUNT_MASTER <= 0;

elsif (CLK' event and CLK ='1') then
if (COUNT_SA = 95555) then
COUNT_SA <= 0;
SA <= not SA;
else
COUNT_SA <= COUNT_SA + 1;
end if;

if (COUNT_RE = 85132) then
COUNT_RE <= 0;
RE <= not RE;
else
COUNT_RE <= COUNT_RE + 1;
end if;

if (COUNT_GA = 75843) then
COUNT_GA <= 0;
GA <= not GA;
else
COUNT_GA <= COUNT_GA + 1;
end if;

if (COUNT_MA = 71586) then
COUNT_MA <= 0;
MA <= not MA;
else
COUNT_MA <= COUNT_MA + 1;
end if;

if (COUNT_PA = 63776) then
COUNT_PA <= 0;
PA <= not PA;
else
COUNT_PA <= COUNT_PA + 1;
end if;

if (COUNT_DHA = 56818) then
COUNT_DHA <= 0;
DHA <= not DHA;
else
COUNT_DHA <= COUNT_DHA + 1;
end if;

if (COUNT_NI = 50620) then
COUNT_NI <= 0;
NI <= not NI;
else
COUNT_NI <= COUNT_NI + 1;
end if;


if (COUNT_SA1 = 47778) then
COUNT_SA1 <= 0;
SA1 <= not SA1;
else
COUNT_SA1 <= COUNT_SA1 + 1;
end if;



if (COUNT_TONE = 25000000) then
COUNT_TONE <= 0;
COUNT_MASTER <= COUNT_MASTER + 1;
else
COUNT_TONE <= COUNT_TONE + 1;
end if;
end if;


if TONE = '0' then
case OCTAVE(COUNT_MASTER) is
when 0 =>
TONE_OUT <= SA;
when 1 =>
TONE_OUT <=RE;
when 2 =>
TONE_OUT <=GA;
when 3 =>
TONE_OUT <=MA;
when 4 =>
TONE_OUT <=PA;
when 5 =>
TONE_OUT <=DHA;
when 6 =>
TONE_OUT <=NI;
when 7 =>
TONE_OUT <=SA1;
when others =>
TONE_OUT <= '0';
end case;
end if;


end process;
end FUNCTIONALITY;
