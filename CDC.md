If 2 FF are asynchronized and have 2 different CLK frequency, then the gap between the two edges will move setup and hold requirements will not be met and may go to metastable state.

Metastability:the value between 0 & 1.

Metastability is harmful to power consumption because the FF will stay in the short circuit on CMOS for longer time.

CDC causes two endpoints with same source point sees different values.

CDC can happen with two CLK with same frequency but has different phase (different PLL)





Double FF Synchronizer:

the output of F1 in next edge will be settled to the intended value then F2 will capture the stable value.

All endpoints should see the same value from only F2 output.

Synchronizers only to avoid the metastability but we need another logic to ensure no data loss. 





Bus Synchronizer:

the group of bits have a problem because some bits may see the old value and the other see the new value due to the difference in routing delay of each bit. different bits may be captured by different FF then each one may be unstable. 



Grey encoding: only1 bit changes every transition therefore the old value stay has meaning.it can be used only if the design follow a pattern such as counter not a random values.



Enabled data: data will be sampled only when enable signal is stable therefore data from F0 bus will have enough time to settle on the bus. this will increase the latency (data sampled by F1 after 3 edges) 



Slow to fast crossing: no data loss happens but frequency difference must be sufficient to avoid setup and hold violations.  



Fast to Slow crossing:

Hand shaking: no loss in data but adds latency to the system.

FIFO: useful if 2 CLK have a very close frequency and data is generating in burst.

it needs extra logic for empty and full flags. Read and write pointers should be synchronized to each other. 

 fifo_full if (wr_fifo && rd_ptr==wr_ptr+1)

fifo_empty if (rd_fifo && wr_ptr==rd_ptr+1)





How to calculate FIFO depth:

calculate the required time for 1 write transactions.
calculate the required time for writing all burst data.
calculate the required time for 1 read transaction.
calculate the number of reads during writing transactions.
FIFO Depth = #Write_Burst_transactions - #Reads_during_Write 
 

 



 
