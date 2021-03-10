# LAB 5

## First task

### Table with connection of push buttons on Nexys A7 board

| **Button** | **Resistor [Ω]** | **PIN** | **Value when pressed + voltage [V]** | 
| :-: | :-: | :-: | :-: |
| BTNL | 10k | P17 | High 3,3 |
| BTNR | 10k | M17 | High 3,3 |
| BTNU | 10k | M18 | High 3,3 |
| BTND | 10k | P18 | High 3,3 | 
| BTNC | 10k | N17 | High 3,3 |

### Table with calculated values

| **Time interval** | **Number of clk periods** | **Number of clk periods in hex** | **Number of clk periods in binary** |
| :-: | :-: | :-: | :-: |
| 2&nbsp;ms | 200 000 | `x"3_0D40"` | `b"0011_0000_1101_0100_0000"` |
| 4&nbsp;ms | 400 000 | `x"6_1A80"` | `b"0110 0001 1010 1000 0000"` |
| 10&nbsp;ms | 1 000 000 | `x"F_4240"` | `b"1111_0100_0010_0100_0000"` |
| 250&nbsp;ms | 25 000 000 | `x"17D_7840"` | `b"0001_0111_1101_0111_1000_0100_0000"` |
| 500&nbsp;ms | 50 000 000 | `x"2FA_F080"` | `b"0010_1111_1010_1111_0000_1000_0000"` |
| 1&nbsp;sec | 100 000 000 | `x"5F5_E100"` | `b"0101_1111_0101_1110_0001_0000_0000"` |

## Second task

### Listing of VHDL code of the process p_cnt_up_down with syntax highlighting

```vhdl
p_cnt_up_down : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then               -- Synchronous reset
                s_cnt_local <= (others => '0'); -- Clear all bits
            elsif (en_i = '1') then       -- Test if counter is enabled
                -- TEST COUNTER DIRECTION HERE
                if (cnt_up_i = '1') then
                 s_cnt_local <= s_cnt_local + 1;
                elsif (cnt_up_i = '0') then
                 s_cnt_local <= s_cnt_local - 1;
                end if;
            end if;
        end if;
    end process p_cnt_up_down;
```

### Listing of VHDL reset and stimulus processes from testbench file tb_cnt_up_down.vhd with syntax highlighting and asserts

```vhdl
    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset_gen : process
    begin
        s_reset <= '0';
        wait for 12 ns;
        -- Reset activated
        s_reset <= '1';
        wait for 73 ns;
        s_reset <= '0';
        wait;
    end process p_reset_gen;
    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        -- Enable counting
        s_en     <= '1';
        -- Change counter direction
        s_cnt_up <= '1';
        wait for 380 ns;
        s_cnt_up <= '0';
        wait for 220 ns;
        -- Disable counting
        s_en     <= '0';
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```

### Screenshot with simulated time waveforms

![simulated time waveforms](Images/waveforms1.JPG)

## Third task

### Listing of VHDL code from source file top.vhd with all instantiations for the 4-bit bidirectional counter

```vhdl

```

### Image of the top layer including both counters, ie a 4-bit bidirectional counter from Part 4 and a 16-bit counter with a different time base from Part Experiments on your own

![simulated time waveforms](Images/waveforms2.JPG)